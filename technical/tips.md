# :bulb: Tips
機械学習ライフサイクルの各ステップにおける Tips をまとめています。
<!-- <details>
<summary> :point_right: 詳細はこちら！ </summary> -->

## 環境構築・運用管理



* **Azure ML Compute Cluster の IP アドレスの枯渇を防ぐ**

    Compute Cluster は仮想ネットワーク VNET を割り当てることができます。VNET の IPアドレスが足りない場合、クラスター起動時に起に失敗するので注意してください。
    - 例 : サブネットが /28 の場合
        - 利用できる IP アドレスは 16 個を利用
        - Azure で 5 つの IP アドレスを利用 (残11)
        - Private Link を利用した場合 2 つの IP アドレスを利用 (残9)
        - Compute Instances, Compute Cluster は１台あたり 1 つの IP アドレスを利用

* **計算リソースのコストを計画・管理する**

    Azure ML で用いる計算リソースはなるべく低コストで運用します。
    - クォータの設定 - Workspace 単位で各 VM タイプごとで利用できるコア数を制限することができます。手順は「[ワークスペースレベルのクォータ](https://docs.microsoft.com/ja-JP/azure/machine-learning/how-to-manage-quotas#workspace-level-quotas)」をご参照ください。
    - Compute Cluster は、`最小ノード数`を 0 にすることで Job が実行されていないときの課金コストを抑えることができます。また`低優先度`オプションを利用するとコストを 80 % 削減できます。
    - Compute Instances には 2021年2月現時点では自動シャットダウンの機能がありません。手動、もしくは Python SDK ([ComputeInstance Class](https://docs.microsoft.com/en-us/python/api/azureml-core/azureml.core.compute.computeinstance.computeinstance?view=azure-ml-py))、Azure CLI ([computeinstance stop](https://docs.microsoft.com/en-us/cli/azure/ext/azure-cli-ml/ml/computetarget/computeinstance?view=azure-cli-latest#ext_azure_cli_ml_az_ml_computetarget_computeinstance_stop)) を用いて停止スクリプトを作成してください。
    - その他、詳細は 「[Azure Machine Learning のコストを計画して管理する](https://docs.microsoft.com/ja-jp/azure/machine-learning/concept-plan-manage-cost)」 をご参照ください。
    - なお、Azure Machine Learning 全体の正確なコスト計算は現在価格表では行えません。例えば Compute Instances で確保されているディスクやロードバランサーなどのコストを加味する必要があります。「[Azure Machine Learning のコスト見積もりについて](https://jpmlblog.github.io/blog/2020/06/18/AML-estimate-costs/)」をご参照ください。



## ETL

* **pyodbc を用いた DB とのやり取り**
    
    Database に格納されているデータを取得する方法として、Azure ML の Dataset ではなく pyodbc を利用したい場合があります。モデル学習時の環境を定義情報を管理する機能として Environment (環境) があります。pyodbc では通常 OS レベルでのパッケージのインストールが必要なため、python のパッケージを pip や conda でインストールだけでは不十分です。下記のコードを参考に Azure ML Environment を作成してください。

    
    
    <details>
    <summary>1. Azure ML Environment の定義 (Python)</summary>

        ```python
        from azureml.core import Workspace, Environment
        from azureml.core.environment import CondaDependencies
        
        # 環境 Environment の名称
        env = Environment("pyodbc-env")

        # Docker File の定義
        dockerfile = r"""
        FROM mcr.microsoft.com/azureml/openmpi3.1.2-ubuntu18.04
        RUN echo "Hello from custom container!"
        
        RUN apt-get update
        RUN apt-get install locales
        RUN locale-gen en_US.UTF-8
        RUN update-locale LANG=en_US.UTF-8
        
        # Install MS SQL v13 driver for Odbc
        RUN apt-get install -y curl
        RUN apt-get install apt-transport-https
        RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add -
        RUN curl https://packages.microsoft.com/config/ubuntu/18.04/prod.list > /etc/apt/sources.list.d/mssql-release.list
        RUN exit
        RUN apt-get update
        RUN ACCEPT_EULA=Y apt-get install -y msodbcsql17
        RUN apt-get install -y unixodbc-dev
        """
        
        # Set base image to None, because the image is defined by dockerfile.
        env.docker.base_image = None
        env.docker.base_dockerfile = dockerfile

        env.python.conda_dependencies = CondaDependencies.create(conda_packages=['scikit-learn','pyodbc'], 
                                                         pip_packages=['azureml-defaults','azureml-dataprep[pandas]'])
        ```
    </details>
    <details><summary>2. Python Script での利用 (Python)</summary>
    

        ```python
        import pandas as pd
        import pyodbc
    
        server = 'tcp:xxxx' 
        database = 'xxxx' 
        username = 'xxxx' 
        password = 'xxxx' 
        cnxn = pyodbc.connect('DRIVER={ODBC Driver 17 for SQL Server};SERVER='+server+';DATABASE='+database+';UID='+username+';PWD='+ password)
        cursor = cnxn.cursor()
        
        sql = """
        SELECT * FROM [dbo].[FactTable]
        """
        df = pd.read_sql(sql, cnxn)
        print(df.head())
        ```

    </details>
    <br>

    参考情報
    - [Azure Machine Learning でソフトウェア環境を作成して使用する](https://docs.microsoft.com/ja-jp/azure/machine-learning/how-to-use-environments)
    - [Microsoft ODBC Driver for SQL Server をインストールする (Linux)](https://docs.microsoft.com/ja-jp/sql/connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server?view=azure-sqldw-latest#ubuntu17)
 
## データ探索

:runner: _coming soon_

## 特徴量エンジニアリング




* **Parquet ファイルで I/O を改善する**

    大きいデータファイルを扱うときは CSV ではなく parquet ファイルの利用をお勧めします。parquet は列指向のファイルフォーマットで圧縮率が高いです。Azure ML の AutoML で大きいデータサイズを扱う際に有効でした。
    - 参考 : [Parquet ファイル形式と CSV ファイル形式](https://docs.microsoft.com/ja-JP/azure/machine-learning/concept-optimize-data-processing#parquet-and-csv-file-formats)


## モデリング



* **モデルの予測値と実測値の誤差を分析する**

    実測値と機械学習モデルの予測値の誤差から新たな知見が得られる場合があります。どういった場合に誤差が発生するのかを分析することに取り組んでください。  
    - [Power BI](https://powerbi.microsoft.com/ja-jp/) による可視化
    - 機械学習モデルの解釈によるデバッグ - 誤差を目的変数にして機械学習モデルを構築し、そのモデルを解釈します。
        - [Power BI の Key Influencers(主要なキーインフルエンサー)](https://docs.microsoft.com/ja-JP/power-bi/visuals/power-bi-visualization-influencers) はマウス操作で誤差に影響していた特徴量を導出できます。(線形回帰、ロジスティック回帰を内部的に利用)
        - [Error Analysis Dashboard](https://github.com/microsoft/responsible-ai-widgets#error-analysis-dashboard) を利用して誤差大きいデータのサブセットを特定することができます。
    
* **ハイパーパラメータチューニングを高速に実行する**

    モデルのハイパーパラメータをチューニングすることによって精度向上が期待できます。Azure Machine Learning では Hyperdrive という機能で提供しています。他にもオープンソースのテクノロジーとの組み合わせも可能です。Compute Cluster 上で並列実行されることで高速に処理することも可能です。
    - [Azure ML Hyperdrive](https://docs.microsoft.com/ja-JP/azure/machine-learning/how-to-tune-hyperparameters) | [Optuna](https://github.com/optuna/optuna) | [Neural Network Intelligence](https://github.com/microsoft/nni) | [FLAML](https://github.com/microsoft/FLAML)


* **実験のスナップショットのサイズに注意する**

    Azure ML ではコードなどのスナップショットを自動保存しますが、300MBを超えるとエラーが出てきます。
    - 対処方法 : `.amlignore`で不要なファイルを指定する
        - 参考ブログ : [Azure Machine Learning に組み込まれた BERT x AutoML で テキスト分類 - Tips](https://qiita.com/dahatake/items/13ec1e277078bc608f3b#1-%E5%AE%9F%E9%A8%93%E3%82%B9%E3%83%8A%E3%83%83%E3%83%97%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88%E3%81%AE%E3%82%B9%E3%83%88%E3%83%AC%E3%83%BC%E3%82%B8%E5%88%B6%E9%99%90)
    - その他の対処方法は「[実験スナップショットのストレージ制限](https://docs.microsoft.com/ja-JP/azure/machine-learning/how-to-save-write-experiment-files#storage-limits-of-experiment-snapshots)」を参照



## 推論

* **推論環境のログを取得する**
    
    推論環境への入力データ、出力データ(予測値)などのログを `Application Insights` に記録することができます。Application Insights の仕様上、64 KB 以上のデータは正常に保存されないので注意してください。
    
    より柔軟にログを残したい場合は、Azure Kubernetes Service のデータ収集機能を利用するか、Blob Storage SDK を用いて直接ストレージに書き込みます。

    - 参考 : [ML Web サービス エンドポイントからのデータを監視および収集する](https://docs.microsoft.com/ja-JP/azure/machine-learning/how-to-enable-app-insights)
    - Blob SDK サンプル : [https://docs.microsoft.com/en-us/samples/azure-samples/azure-sdk-for-python-storage-blob-upload-download/upload-download-blobs-python/](https://docs.microsoft.com/en-us/samples/azure-samples/azure-sdk-for-python-storage-blob-upload-download/upload-download-blobs-python/)


## MLOps

* **Azure Machine Learning CLI を使って CI/CD を構築する**

    Azure CLI の Azure ML 拡張機能である Azure Machine Learning CLI を使うと、Python コードをそのまま実行するよりも CI/CD の実装がシンプルになります。「[コマンドラインでの機械学習 (Zenn)](https://zenn.dev/keonabut/articles/42bd1924ccd882)」をご参照ください。

## 責任のある AI 

* **説明性・解釈性が求められるケースでは、シンプルなモデルの利用も考える**

    与信管理・製造の品質管理・メディカルなどでは機械学習モデルの説明・解釈性が重要です。そのようなケースでは、ニューラルネットワークやアンサンブル手法ではなく、解釈性の高いモデルの利用を考えます。例としては、線形回帰モデルや Microsoft Research が主導で開発している [Explainable Boosting Model](https://github.com/interpretml/interpret) という一般化加法モデルの推定アルゴリズムが挙げられます。

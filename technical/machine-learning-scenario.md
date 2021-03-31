#  :white_check_mark: Well-Architected Framework Assessment for Machine Learning
機械学習ワークロードにおける Well Architected Framework のアセスメント

**コスト最適化**、**オペレーション・エクセレンス**、**パフォーマンス効率**、**信頼性**、**セキュリティ** の軸でのアセスメント

[<img src="./images/assessment.png" title="assessment" width="250">](WAF/machine-learning-scenario.md)
<br>
<!-- :point_right: **[アセスメントシート](WAF/machine-learning-scenario.md)** -->
    
※ こちらはあくまで一般的な推奨事項に関する確認であり、お客様の要件に応じて柔軟に対応していく必要があります。
    
※ Azure 全般については [Microsoft Azure Well-Architected Review](https://aka.ms/architecture/review) を参照ください。

!> [前提条件]
本ページでは Azure Machine Learning を中心とした機械学習シナリオに特化した Well Architected Framework のアセスメントを行います。機械学習システム全体の観点では当然ながら Azure Machine Learning 以外のサービスやアプリケーションも考慮する必要がありますが、本ページでは割愛しています。

<!-- ## Tables of Contents
- [オペレーショナルエクセレンス](#オペレーショナルエクセレンス)
- [パフォーマンス効率](#パフォーマンス効率)
- [コスト最適化](#コスト最適化)
- [信頼性](#信頼性)
- [セキュリティ](#セキュリティ) -->

---
## オペレーショナルエクセレンス

### Applicaiton Design
- [ ] 実験のメトリックを収集していますか？
- [ ] Azure Machine Leanring のアップデートを定期的に確認していますか？
    - [Azure Machine Learning Release Notes](https//docs.microsoft.com/en-us/azure/machine-learning/azure-machine-learning-release-notes) を確認ください。
    
### Health Modeling & Monitoring
- [ ] モデル学習の成功・失敗の通知をキャチしていますか？
    - Azure Machine Learning は Azure Event Grid を利用してイベントを Teams で通知するなど、様々なシステムに連携することができます。[Azure Machine Learning イベントに基づいてアプリケーション、プロセス、または CI/CD ワークフローをトリガーする (プレビュー)](https://docs.microsoft.com/ja-jp/azure/machine-learning/how-to-use-event-grid) を参照ください。

- [ ] モデルのデプロイの成功・失敗の通知をキャッチしていますか？
    - Azure Machine Learning は Azure Event Grid を利用してイベントを Teams で通知するなど、様々なシステムに連携することができます。[Azure Machine Learning イベントに基づいてアプリケーション、プロセス、または CI/CD ワークフローをトリガーする (プレビュー)](https://docs.microsoft.com/ja-jp/azure/machine-learning/how-to-use-event-grid) を参照ください。


### Security & Compliance
- [ ] 個人情報を扱うことや利用ユーザに大きな影響を与えるセンシティブなシナリオで AI を利用する場合、社内で審議するための明確なプロセスはあるか？
    - 例えば Microsoft では AETHER 委員会、Office of Responsible AI (ORA) など AI の倫理などの責任のある AI の方針や問題に対処するための仕組みがあります。[Microsoft AI Business School](https://www.microsoft.com/ja-JP/ai/ai-business-school) で Microsoft 取り組みについて学習いただき自社にて活用ください。

### Operational Procedures
- [ ] 障害発生時などに運用されているものと同じ機械学習モデルや推論環境を自動パイプラインで構築できますか？
    - Github Actions や Azure Pipelines を用いて CI/CD パイプラインを構築し、推論環境を構築しておくことで、推論環境が構築されるまでのプロセスが明確になり、再現環境を構築することができます。

### Deployment & Testings
- [ ] どのように推論環境をデプロイしていますか？どのくらいの時間がかかりますか？
    - 適宜人のレビューは必要ですが、なるべく自動化することで、効率的にデプロイメントを行うことができます。障害があった場合などに素早く対応できるためにも短い時間でデプロイが完了するようにプロセスを調整する必要があります。

### Operational Model & DevOps
- [ ] MLOps の概念をベースに実験・運用管理プロセスが設計されていますか？
    - MLOps は DevOps を機械学習ワークロードに対応させてものです。Data Scientist と IT Professional が連携して、素早くシステムを構築したり修正することができるようになり俊敏性と効率を向上させることができます。Microsoft の MLOps のアプローチについては [Machine Learning Operations](https://azure.microsoft.com/ja-jp/services/machine-learning/mlops/) を参照ください。

- [ ] 完成した機械学習モデルは再現可能な形で運用チームに引き渡されているか？
    - Data Scientist が開発した機械学習モデルが再現できず、デプロイメントが成功しないことがあります。Data Scientist はモデル開発が再現できるように、データ、コード、Python 環境情報などのアセットを適切に管理する必要があります。

- [ ] 機械学習モデルの精度劣化やデータドリフトが見受けられた場合に、開発チームと運用チームはどのような体制で問題を解決しますか？
    - まず精度劣化やデータドリフトが発生したことを通知する仕組みを Azure Machine Learning + Azure Event Grid などの仕組みで構成します。精度劣化やデータドリフトには様々な原因が考えられるため、関係者を巻き込んで調査・対応できる社内体制とプロセスを作成しておく必要があります。

---

## パフォーマンス効率
### Applicaiton Design
- [ ] モデルの推論で必要な CPU コア数やメモリは見積もられているか？
    - 適切なコア数、メモリで推論環境が構成されていない場合、レスポンス時間が長くなったり、タイムアウトする可能性があります。Azure Machine Learning では Azure Container Instances が仮想ネットワークで構成されていない場合にプロファイル機能が利用できます。[モデルをプロファイルしてリソース使用状況を判断する](https://docs.microsoft.com/ja-JP/azure/machine-learning/how-to-deploy-profile-model?pivots=cli) をご参照ください。

- [ ] モデル学習を高速に行うために Spark などの分散処理や GPU は利用されているか？
    - 大規模データをハンドリングするときは通常のシングルノードでの処理では学習に時間がかかる恐れがあります。Spark などの分散処理、Nvidia RAPIDS などの GPU 環境の利用などを検討する必要があります。

### Health Modeling & Monitoring
- [ ] 推論環境の CPU 利用率などのメトリックは収集されますか？
    - 本番で運用されている推論環境のパフォーマンスを定期的に確認し、問題が発生していないか、レスポンス時間は想定通りかを確認して、継続的な推論環境の改善に取り組む必要があります。

### Capacity & Service Availability
- [ ] 実験環境を利用する需要や稼働率が上限に達するほどに高くなることはありますか？
    - 処理負荷が一定でなくバラ付きがある場合は Azure Machine Learning の Compute Cluster を利用することで、リソース不足に陥ることなくジョブを実行することができます。予めクォータを確保しておき、最大ノード数が最大負荷に耐えうるように設定しておく必要があります。
### Application Platform Availability
- [ ] 推論環境は高可用性を考慮した設定になっていますか？
    - Azure Kubernetes Service にデプロイすることで Kubernetes の高可用性の恩恵を享受できます。また、Azure Machine Learning Pipeline でバッチ推論を行う場合においても、Azure Data Factory や Synapse Pipeline を利用すれば Fail しても再試行することができます。

### Data Platform Availability
- [ ] データソースは高可用性を考慮した設定になっていますか？
    - Azure SQL Database などは高可用性が構成できるようになっています。利用しているサービスごとに設定を確認してください。

### Scalability & Performance
- [ ] 推論環境はスケーラビリティが考慮されていますか？
    - Azure ML の Web API 形式の推論として Azure Kubernetes Service が選択できます。高いスケーラビリティが要求される場合には最適です。一方でバッチ推論の形式については Azure Machine Learning Pipeline を利用します。Pipelien の計算環境として Compute Cluster が選択できるため、こちらも高いスケーラビリティが実現できます。

### Deployment & Testings
- [ ] 機械学習モデルの軽量化・高速化は行われているか？
    - 推論環境でのモデルがメモリを消費し、同居する他のアプリケーションにパフォーマンスの影響をもたらす場合があります。特に Edge デバイスでモデルを運用する際は、Edge デバイスのスペックが制限されている場合があり考慮が必要です。Microsoft などで開発している ONNX はあらゆる API に対応した業界スタンダードのオープンソースのモデルフォーマットです。[ONNX と Azure Machine Learning:ML モデルの作成と能率化](https://docs.microsoft.com/ja-JP/azure/machine-learning/concept-onnx) jをご参照ください。

- [ ] 推論環境を Web API で公開している場合、期待される時間内に予測値は返ってきますか？タイムアウトが発生するリスクはありますか？
    - 推論の処理が遅延することで、関係するアプリケーションに影響したり、ユーザーエクスペリエンスを低下させます。本番稼働させる前に十分にテストする必要があります。また改善方法として ONNX の活用、機械学習アルゴリズムの見直し、ハイパーパラメータの見直しなどを検討してください。

- [ ] バッチ推論のジョブは期待される時間内に完了しますか？
    - 夜間のバッチ処理で予測値を算出するようなシナリオにおいて、想定以上のデータが入力されることによる遅延や、(特に DWH において) 他システムとの処理の競合により遅延などが懸念されるため、十分にリソースや実行タイミングを計画してください。


### Performance Testing
- [ ] モデル学習時でのパフォーマンスをモニタリングしていますか？
    - [kineto](https://github.com/pytorch/kineto) などを利用するとモデル学習におけるパフォーマンスの監視やそれに基づく対処が可能になります。

- [ ] 推論環境でのパフォーマンスはテストは実行されていますか？
    -  Model Profile 機能を利用すると Azure Container Instances で必要な CPU コア数・メモリ量が見積もれます。[モデルをプロファイルしてリソース使用状況を判断する](https://docs.microsoft.com/ja-JP/azure/machine-learning/how-to-deploy-profile-model?pivots=cli) をご参照ください。

### Troubleshooting
- [ ] 機械学習パイプラインの処理速度のボトルネックはどこにありますか？
    - 予めパイプラインの各モジュールにおける想定される実行時間を見積もっておきます。Azure Machine Learning Pipeline ではパイプラインの各モジュールで動作する計算環境をそれぞれ指定できるため、処理速度が懸念されるモジュールには高スペックの計算環境を付与するなど対処してください。

- [ ] 推論環境のメモリ消費量や CPU 利用率などをモニタリングしていますか？
    - CPU 利用率やメモリ消費量をモニタリングし、必要に応じて実装方法を変更します。また計算環境のスケールアップ (垂直)、スケールアウト (水平) の仕組みの導入を検討します。

---

## コスト最適化 
### Applicaiton Design
- [ ] 利用シナリオに対してモデルの精度要件が明確に定義されていますか？
- [ ] モデルを軽量化することで推論環境の節約をしていますか？
    - ONNX を用いてモデルを軽量化することができます。一方、軽量化することでモデル精度が劣化するため、トレードオフを考慮する必要があります。[ONNX と Azure Machine Learning:ML モデルの作成と能率化](https://docs.microsoft.com/ja-JP/azure/machine-learning/concept-onnx) jをご参照ください。

### Health Modeling & Monitoring
- [ ] 推論環境のメモリ消費量や CPU 利用率などをモニタリングしていますか？
    - CPU 利用率やメモリ消費量をモニタリングし、必要に応じて実装方法を変更します。余力があれば推論環境のスペックを下げます。またオンデマンド型のサービスに切り替えて運用することで、トラフィックがない時間帯のコストを削減することが可能です。

### Networking & Connectivity
- [ ] 大規模データの移動が発生しますか？
    - リージョン間、クラウドベンダー間、Private Link におけるデータの送受信におけるコストを考慮する必要があります。

### Operational Procedures
- [ ] 利用していない学習環境やテスト用の推論環境を定期的にチェックしていますか？
    - Azure Monitor などの監視の仕組みを利用して、定期的にリソースの利用状況を把握してください。[Azure Machine Learning の監視](https://docs.microsoft.com/ja-JP/azure/machine-learning/monitor-azure-machine-learning) をご参照ください。

- [ ] 自動シャットダウンの機能を有効にしていますか？
    - Compute Cluster は最小ノード数と最大ノード数が設定でき、最小ノード数を 0 にするとジョブがない時に自動で計算環境をシャットダウンします。

### Efficiency and Sizing
- [ ] モデル学習のワークロードに応じて低優先度オプションを使い分けていますか？
    - Compute Cluster の低優先度オプションは、Azure データセンターの余剰リソースを活用できる機能です。ジョブが途中で中断されるリスクはありますが、許容できるようなハイパーパラメータチューニングなどワークロードにおいては利用を検討してください。[優先順位の低い VM を使用する](https://docs.microsoft.com/ja-JP/azure/machine-learning/concept-plan-manage-cost#use-low-priority-vms) をご参照ください。

---

## 信頼性
### Model Design
- [ ] 機械学習モデルの説明性・解釈可能性は考慮されていますか？
    - ニューラルネットワークなどの複雑なモデルは一般的には精度が高いものの、説明性・解釈可能性が劣ります。そのためシステム導入にあたってステークフルダーに対してモデルの理解が得られない、デバッグが難しい、予測根拠が分からないなとの懸念があります。[InterpretML](https://interpret.ml/) を用いることで、解釈可能性が高い推定アルゴリズムや SHAP などをベースにした説明性を実現できます。
    
- [ ] 機械学習モデルの公平性は考慮されていますか？
    - 人種や性別などによってモデル学習の挙動が異なることが問題となるケースがあるため注意が必要です。[Fairlearn](https://fairlearn.org/) を用いることで、_公平性の評価_ と _不公平性の軽減モデルの構築_ ができます。
    
- [ ] 機械学習モデルのプライバシー保護は考慮されていますか？
    - 学習データに個人情報などのプライバシーデータが含まれる場合、その情報がモデルからリークする恐れがあります。[差分プラバシー](https://docs.microsoft.com/ja-jp/azure/machine-learning/concept-differential-privacy) を用いて、データにノイズやランダム性を追加してデータが特定されることを防ぐことができます。
    
- [ ] 機械学習システムは人間中心のデザインになっていますか？
    - AI は確率的な挙動をするなど従来のソフトウェアとな特性が変わってきます。人間と AI の相互作用について考慮したデザインが必要です。[Guildelines for Human-AI Interaction](https://www.microsoft.com/en-us/research/project/guidelines-for-human-ai-interaction/) にガイドラインが記載されています。
 
- [ ] 利用シナリオに対して、モデル精度や発生しうる誤差について、利用ユーザと共通認識がありますか？
    - 機械学習モデルは確率的な動きをするため必ずしも 100% 期待した結果 (精度) になるとは限りません。予め利用するモデルの精度や想定される挙動はステークホルダーと同意しておく必要があります。[Error Analysis](https://erroranalysis.ai/) を利用することで、モデルの誤差の分析を行うことができ、効率的にモデルの挙動を把握することができます。

- [ ] 学習コードや推論コードのコード規約は確認していますか？
    - Lineter を用いて Python コードをチェックします。VSCode で利用可能な Linter は、[Linting Python in Visual Studio Code](https://code.visualstudio.com/docs/python/linting#_specific-linters) より確認できます。

### Health Modeling & Monitoring
- [ ] デプロイしたモデルの精度の変化はモニタリングしていますか？
    - 運用中のモデルの精度が確認できる場合は、精度をモニタリングします。必要に応じて再学習・再実験を行い推論環境を改善していく必要があります。
    
- [ ] デプロイしたモデルに関連するデータ分布はモニタリングしていますか？
    - 運用中のモデルの精度が算出できない場合はデータの分布を確認します。モデル学習時のデータ分布と運用中のデータ分布を比較して差が大きくなっている場合は精度が低下していることが想定されます。[ドリフト検知 (プレビュー)](https://docs.microsoft.com/ja-JP/azure/machine-learning/how-to-monitor-datasets?tabs=python)を用いて自動的にアラートを出すことが可能です。

### Capacity & Service Availability
- [ ] 本番で環境で Azure サービスの Preview 機能は利用していますか？
    - Preview 機能は SLA やサポート範囲が限定されるため注意が必要です。
    
- [ ] 学習環境の将来定な需要の変化を把握・予測していますか？
    - Azure ML Compute Instances / Compute Cluster を稼働させるためのクォータを確保することができます。

### Application Platform Availability
- [ ] 推論環境は高可用性の構成になっていますか？
    - 高可用性が求められるシナリオで、API での推論環境を構築される場合は、Azure Kubernetes Service の利用を推奨します。詳細は、Azure Kubernetes Service のドキュメント 「[Azure Kubernetes Service (AKS) での事業継続とディザスター リカバリーに関するベスト プラクティス](https://docs.microsoft.com/ja-jp/azure/aks/operator-best-practices-multi-region)」と「[可用性ゾーンを使用する Azure Kubernetes Service (AKS) クラスターを作成する](https://docs.microsoft.com/ja-jp/azure/aks/availability-zones)」を参照ください。 Azure Machine Learning 経由で Azure Kubernetes Service のクラスターを作成した場合は、複数リージョンでの高可用性はサポートされません。


### Scalability & Performance
- [ ] モデル学習は期待された時間内に完了しますか？
    - データサイズが大きかったり、機械学習アルゴリズムが複雑な場合には学習時間が長くなります。その場合は、サンプリングして学習データを減らしたり、Spark などの並列処理、GPU での処理などを検討ください。([Azure Machine Learning を使用したデータ処理の最適化](https//docs.microsoft.com/ja-JP/azure/machine-learning/concept-optimize-data-processings))
    
- [ ] モデル推論は期待された時間内に完了しますか？
    - ストリーミングデータに対する推論などリアルタイム性が求められる推論は Web API、大量データに対する定期的な推論はバッチ推論の形態を採用します。
    
- [ ] 学習データの増加率は予測していますか？
    - データソースのサイズやモデル学習環境のスペックを決定するために、今後データサイズの増加率を評価しておく必要があります。
     
- [ ] モデル学習環境の自動スケールは有効にしていますか？
    - Azure ML Compute Cluster はスケールアウト/ダウンが可能なクラスター環境です。最小ノード数と最大ノード数の設定可能です。定常的なワークロードでなく、求められるパフォーマンスが可変の場合は特に利用をお勧めします。Compute Cluster の詳細は、[Azure Machine Learning コンピューティング クラスターの作成
](https://docs.microsoft.com/ja-JP/azure/machine-learning/how-to-create-attach-compute-cluster?tabs=python#what-is-a-compute-cluster) をご参照ください。

### Security & Compliance
プライバシー保護、White Noise、説明性・解釈可能性
- [ ] Azure Active Directy の "多要素認証" や "条件付きアクセス" は有効にしていますか？
    - 多要素認証・条件付きアクセスによってよりセキュアな認証が可能になります。

- [ ] ユーザごとに適当にロールを定義していますか？
    - RBAC を利用して Azure ML を利用するユーザにロールベースのアクセス制御を行います。設定方法は、[Azure Machine Learning ワークスペースのアクセス管理](https://docs.microsoft.com/ja-JP/azure/machine-learning/how-to-assign-roles) をご参照ください。

- [ ] 脆弱性のチェックはしていますか？
    - [Azure Security Center](https://docs.microsoft.com/ja-jp/azure/security-center/security-center-introduction) において Azure Container Registry と Azure Kubernetes Service のリソースに対するスキャンを有効化してください。
    
- [ ] Azure Machine Learning へのアクセスは仮想ネットワークで保護されていますか？
    - Private Link や Service Endpoint を利用して関連リソースを仮想ネットワークに配置したり、Workspace へのアクセスを特定の仮想ネットワークからに限定することができます。

### Operational Procedures

- [ ] 実験に用いた学習データ、コード、Python環境情報、パラメータは適切に管理されていますか？
    - Azure MAchine Learning の [Experiment 機能](https://docs.microsoft.com/ja-jp/azure/machine-learning/how-to-monitor-view-training-logs) を利用すれば実験時のメトリック、ログ、モデル、学習データ、Python 環境情報などの情報を記録することができます。またコードもスナップショットして保存されますし、git 連携されているコードであれば、コードの git の URL や Commit 番号を一緒に紐付けできます。最低でも推論環境で利用するモデル開発時の記録は取っておくことを推奨します。

- [ ] 現在利用されている推論環境やその前のバージョンの推論環境を再度構築することができますか？
    - Github Actions や Azure Pipelines を用いて CI/CD パイプラインを構築し、推論環境を構築しておくことで、推論環境が構築されるまでのプロセスが明確になり、再現環境を構築することができます。

### Deployment & Testings
- [ ] 業務システムと連携している本番の推論環境はどのくらいありますか？その推論環境へのモデルのデプロイは (ある程度) 自動化されていますか？
    - Github Actions や Azure Pipelines を用いて CI/CD パイプラインを構築し、デプロイを自動化できます。

- [ ] モデルの再学習を現在行っていますか？また将来的に実施する予定ですか？その場合、再学習されたモデルの評価においてデグレは考慮されていますか？
    - データの変化、ユーザのニーズの変化によって、モデルの再学習が必要になることがあります。定期的にモデルをモニタリングし、再学習・再実験するフローを確立しておきます。
    
- [ ] ミッションクリティカルなシステムにおいて、Blue/Green や Canary デプロイメントを利用していますか？
    - Blue/Green や Canary デプロイメントは、利用ユーザへの影響を最小限に留めて新しい機能や変更を徐々にリリースする方法です。Azure Machine Learning としては Azure Kubernetes Serivce において Controlled Rollout (Preview) を提供しており、複数バージョンのエンドポイントへのトラフィック量を制御することができます。[制御されたロールアウト (プレビュー) を使用して AKS にモデルをデプロイする](https://docs.microsoft.com/ja-JP/azure/machine-learning/how-to-deploy-azure-kubernetes-service?tabs=python#deploy-models-to-aks-using-controlled-rollout-preview) をご参照ください。
---

## セキュリティ
### Applicaiton Design
- [ ] GDPR などの規制に対応していますか？
    - Azure Machine Learning では Workspace のデータのダウンロードとアーカイブ・削除が行えます。[Machine Learning service のワークスペース データをエクスポートまたは削除する
](https://docs.microsoft.com/ja-jp/azure/machine-learning/how-to-export-delete-data) をご参照ください。

- [ ] Azure Policty をセキュリティ、コンプライアンス、組織標準を適用するために使用していますか？
    - Azure Policy は Azure の各サービスがポリシーに準拠させることができます。Azure Machine Learning の Azure Policy の概要は [Azure Policy を使用した Azure Machine Learning の監査と管理](https://docs.microsoft.com/ja-jp/azure/machine-learning/how-to-integrate-azure-policy) を参照ください。利用できる Python パッケージを限定したり (Preview)、Private Link の利用を強制することができます。([組み込み Policy 一覧](https://docs.microsoft.com/ja-jp/azure/machine-learning/how-to-integrate-azure-policy))

- [ ] 機械学習で利用しているオープンソースのフレームワークやライブラリを管理していますか？
    - フレームワークやライブラリに起因する脆弱性が問題なるケースがあります。Azure Security Center を用いて Azure Container Registry や Azure Kubernetes Service のスキャンを有効にすることを推奨します。

### Health Modeling & Monitoring
- [ ] PII や機密データは機械学習のプロセスの中でどのように検知され、対処 (削除/難読化) されますか？
    - データカタログソリューションである Azure Purview を用いてデータソースに対するスキャンとデータ分類を実行することができます。また、[Azure Text Analytics の PII 検出機能](https://westus2.dev.cognitive.microsoft.com/docs/services/TextAnalytics-v3-1-preview-3/operations/EntitiesRecognitionPii) や OSS の PII 検知機械学習モデル [presidio](https://github.com/microsoft/presidio) の利用も検討ください。
    
### Networking & Connectivity
- [ ] Azure PaaS サービスに接続する際に Private Link や Service Endpoint は利用していますか？
    - 特定の仮想ネットワークからのアクセスに制御し、インターネットからの通信を遮断することでよりセキュアな環境になります。[仮想ネットワークの分離とプライバシーの概要
](https://docs.microsoft.com/ja-jp/azure/machine-learning/how-to-network-security-overview) を参照ください。

### Security & Compliance
- [ ] 機密データを取り扱う場合、TEE や準同型暗号などの暗号化を利用していますか？
    - [Azure Confidential Computing](https://azure.microsoft.com/ja-jp/solutions/confidential-compute/) は Intel SGX を搭載しており、Enclave 内部でセキュアな計算処理を実行できます。また、[Microsoft SEAL](https://github.com/microsoft/SEAL) は Microsoft が開発している準同型暗号のライブラリで、このライブラリに対応した機械学習ライブラリを利用することで、データを暗号化したまま計算処置が実行できます。非常に高いセキュリティ要件の場合は利用を検討ください。
    
- [ ] 学習コードや推論コードで利用するパスワードなどのシークレットは Azure Key Vault に格納していますか？
    - シークレットをコードに直に記載すると安全ではありません。Azure Machine Learning のリソースにもある Azure Key Vault にシークレットを保存して、コードの中で呼び出すようにしてください。[Azure Machine Learning トレーニングの実行で認証資格情報シークレットを使用する
](https://docs.microsoft.com/ja-jp/azure/machine-learning/how-to-use-secrets-in-runs) をご参照ください。

### Deployment & Testings

- [ ] CI パイプラインにおいてコードの脆弱性のチェックは行われていますか？
    - Github、Azure DevOps またはオープンソースのライブラリにコードの脆弱性をスキャンする機能があります。

- [ ] CI/CD パイプラインにおいて資格情報、証明書、およびその他シークレットはセキュアに管理されていますか？
    - Azure Key Vaults のシークレット管理機能や、Azure DevOps や Github から提供されている Secret 機能などを利用し、極力コードに直接シークレット情報を記載しないようにします。
 
### Operational Model & DevOps
- [ ] CI/CD パイプラインに関与する人の役割の定義とアクセス許可の設定はできていますか？
    - 機械学習には様々な役割を担う人が参画します。それぞれの役割ごとのリソースに対するアクセス許可・不許可、実行許可・不許可の設定を正しく行っておく必要があります。

### Identity & Access Control
- [ ] 機械学習に関与する人ごとに適切なロールが設定されていますか？
    - Azure Machine Learning では内部のリソースごとに RBAC が設定できます。[Azure Machine Learning ワークスペースへのアクセスの管理](https://docs.microsoft.com/ja-jp/azure/machine-learning/how-to-assign-roles) にサンプルのロールの記載があります。

---




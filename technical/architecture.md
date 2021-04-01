## Azure 全体アーキテクチャ
* [Azure Architecture Center](https://docs.microsoft.com/ja-JP/azure/architecture/data-guide/big-data/ai-overview) - ユースケース毎のリファレンスアーキテクチャ集
    - [AI + 機械学習](https://docs.microsoft.com/ja-jp/azure/architecture/data-guide/big-data/ai-overview) - リファレンスアーキテクチャ、ソリューションがを公開
        - [Azure Machine Learning を利用しているアーキテクチャ例](https://docs.microsoft.com/ja-jp/azure/architecture/browse/?expanded=azure&products=azure-machine-learning)


## Azure Machine Learning アーキテクチャ
Azure Machine Learning は他の Azure サービスと一緒に構成されます。

**Workspace**

<img src='https://docs.microsoft.com/en-us/azure/machine-learning/media/concept-azure-machine-learning-architecture/architecture.svg' width=500 />

※ IT 管理者は、[Azure Machine Learning のしくみ:アーキテクチャと概念](https://docs.microsoft.com/ja-JP/azure/machine-learning/concept-azure-machine-learning-architecture) を一読ください。

<br>

**仮想ネットワーク構成(学習)**
特定の仮想ネットワークからのみ Azure Machine Learning Workspace へのアクセスさせたい場合は、**Private Link & Endpoint** の構築が必須です。

<img src='https://docs.microsoft.com/ja-jp/azure/machine-learning/media/how-to-network-security-overview/secure-training-environment.png' width=500>

**仮想ネットワーク構成(推論)**
Azure Kubernetes Services (AKS) 利用時の構成です。
<img src='https://docs.microsoft.com/ja-jp/azure/machine-learning/media/how-to-network-security-overview/secure-inferencing-environment.png' width=500>

<br><br>


## Data Ingestion Pattern

:construction:	under construction !

**参考ドキュメント**
- [Azure Data Factro を使用したデータインジェスト](https://docs.microsoft.com/ja-jp/azure/machine-learning/how-to-data-ingest-adf)
- [Azure Synapse を使用したデータ準備](https://docs.microsoft.com/ja-jp/azure/machine-learning/how-to-data-prep-synapse-spark-pool)
- [データインジェクトパイプラインの DevOps](https://docs.microsoft.com/ja-JP/azure/machine-learning/how-to-cicd-data-ingestion)
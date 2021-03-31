# :pencil: サンプル実装
## Azure Machine Learning 
- [Azure Machine Learning サンプルコード (Community)](https://github.com/Azure/azureml-examples) - 開発者コミュニティによって Contribute されているテクノロジーごとのサンプルコード集
- [Azure Machine Learning サンプルコード (公式)](https://github.com/Azure/MachineLearningNotebooks) - Azure Machine Learning の機能別の公式サンプルコード集
- [Azure Machine Learning Gallery](https://github.com/Azure/AzureMachineLearningGallery) - Azure ML Designer のカスタムモジュールを作成するサンプルコード
- [Auzre ML 2.0 Developer Experience](https://github.com/Azure/azureml-v2-preview) - Azure ML 2.0 API/CLI/SDK (private preview)
- Many Models Solution Accelerator ([英語](https://github.com/microsoft/solution-accelerator-many-models) / [日本語](https://github.com/c-nova/solution-accelerator-many-models)) - 大量のモデル構築・推論の実装テンプレート
- [Factory AI Vision](https://github.com/Azure-Samples/azure-intelligent-edge-patterns/tree/master/factory-ai-vision#custom-vision--azure-iot-edge-for-factory-ai) - 工場における Edge AI の実装テンプレート

<br>

## ユースケース観点


|ユースケース         |ソリューション      |サンプルコード  |
|------------------|------------------|---------|
| Computer Vision   | 医療画像の分類、セグメンテーション | [Project InnerEye](https://github.com/microsoft/InnerEye-DeepLearning)|
||地震層相画像のセグメンテーション| [Deep Seismic](https://github.com/microsoft/seismic-deeplearning)|
||姿勢推定| [Computer Vision Receips](https://github.com/microsoft/computervision-recipes)|
|Personalize        |商品のレコメンデーション|[Azure Synapse Solution Accelerator Retail Recommender](https://github.com/microsoft/Azure-Synapse-Retail-Recommender-Solution-Accelerator)|
||協調フィルタリング、コンテンツベースフィルタリング、ハイブリッド| [Microsoft Recommenders](https://github.com/microsoft/computervision-recipes)([日本語訳](https://github.com/c-nova/recommenders)) |
|Predictive Maintenance     |設備故障 (設備耐用年数) の予測     |[DeepLearning-Workshop](https://github.com/konabuta/DeepLearning-Workshop/blob/ff71b9a630fc1691f10bfba420d76ee0b90fa3de/Sample/Keras/Keras-LSTM-PredictiveMaintenance-datastore-Hyperdrive.ipynb)         |
|Autonomous System  |ビル空調の運転最適化         |[bonsai-simulink](https://github.com/microsoft/bonsai-simulink/tree/main/samples/building_energy_management)         |
||化学プラントにおける製造工程最適化      |[bonsai-simulink](https://github.com/microsoft/bonsai-simulink/tree/main/samples/building_energy_management)         |
|Churn Analysis     |退職予測とモデル解釈         | [Responsible AI Widgets - Samples](https://github.com/microsoft/responsible-ai-widgets/blob/main/notebooks/interpretability-dashboard-employee-attrition.ipynb)        |
|Customer Analytics |差分プライバシーによる合成データを用いた年収予測モデルの開発 | [SmartNoise - Samples](https://github.com/opendp/smartnoise-samples/blob/602ecd926c47b891d91009fe2050645d101ca1a1/data/synthesis/mwem_sample/Adult%20Dataset%20Classification%20(Binary).ipynb) |
||年収予測モデルの開発と公平性の評価と軽減| [Responsible AI Widgets - Samples](https://github.com/microsoft/responsible-ai-widgets/blob/main/notebooks/fairness-dashboard-loan-allocation.ipynb)|
||後方互換性を考慮した年収予測モデルの開発|[Backward Compatibility ML - Samples](https://github.com/microsoft/BackwardCompatibilityML/blob/dev/examples/compatibility-analysis-adult.ipynb)|
||患者のガン診断モデルと影響した変数の抽出|[InterpretML - Samples](https://github.com/interpretml/interpret-community/blob/master/notebooks/explain-binary-classification-local.ipynb)|
|Text Analytics     |Livedoor ニュース記事の分類|[AzureML-NLP (日本語)](https://github.com/konabuta/AzureML-NLP)         |
|Credit Analytics   |住宅ローンの与信モデル構築と反実仮想サンプルの生成 | :runner: _under construction_ ([DiCE](https://github.com/interpretml/DiCE)をベースに作成中)         |
|Demand Forecasting |時系列予測 (統計手法、機械学習、真相学習)|[Forecasting Best Practices](https://github.com/microsoft/forecasting)|
||各商品ブランドの店舗ごとの大量モデル開発と推論| [Many Models Solution Accelerator](https://github.com/microsoft/solution-accelerator-many-models)|
|Anomaly Detection  |ビデオの異常検知 (教師あり、教師なし)         | [MLOps_VideoAnomalyDetection](https://github.com/microsoft/MLOps_VideoAnomalyDetection)        |
||不正アクセス検知|[MMLSpark](https://github.com/Azure/mmlspark/blob/master/notebooks/samples/CyberML%20-%20Anomalous%20Access%20Detection.ipynb)|

<br>

## サンプルコード・ハンズオンコンテンツ
<details>
<summary> details </summary>

- [azureml-hybrid](hhttps://github.com/konabuta/azureml-hybrid) - Azure Machine Learning をローカル環境とクラウド環境での利用ハンズオンコンテンツ
- [azureml-mlops](https://github.com/konabuta/azureml-mlops) - MLOps ハンズオンコンテンツ (Github Actions & Azure Pipelines 連携)
- [AutoML-Pipeline](https://github.com/konabuta/AutoML-Pipeline) - AutoML パイプラインのエンドツーエンドのサンプルコード

</details>

## その他
- [Microsoft Japan Code Labs](https://microsoft.github.io/code-labs-jp/) - ハンズオンコンテンツ (日本マイクロソフトが収集)。AI や Analytics フィルタリングできます。
- [Azure Samples (GitHub)](https://github.com/Azure-Samples) - Azure のサンプルコード集


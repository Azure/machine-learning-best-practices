# :pencil: サンプル実装
## Azure Machine Learning 
- [Azure Machine Learning サンプルコード (Community)](https://github.com/Azure/azureml-examples) - 開発者コミュニティによるテクノロジー別のサンプルコード集

- [Azure Machine Learning サンプルコード (公式)](https://github.com/Azure/MachineLearningNotebooks) - Azure Machine Learning の機能別の公式サンプルコード集

- [Azure Machine Learning Gallery](https://github.com/Azure/AzureMachineLearningGallery) - Azure ML Designer のカスタムモジュールを作成するサンプルコード

- [Azure ML 2.0 Developer Experience](https://github.com/Azure/azureml-v2-preview) - Azure ML 2.0 API/CLI/SDK (private preview)

- [AutoML for Computer Vision](https://github.com/swatig007/automlForImages) - sample code of automl for computer vision tasks (classification, object detection, instance segmentation)


## Solution Accelerators
- [Azure Synapse Solution Acceleartor Retail Recommender](https://github.com/microsoft/Azure-Synapse-Retail-Recommender-Solution-Accelerator) - Retail におけるレコメンデーションシステムの実装テンプレート

- [Financial Analytics Customer Revenue Growth Factor Solution Accelerator](https://github.com/microsoft/Azure-Synapse-Solution-Accelerator-Financial-Analytics-Customer-Revenue-Growth-Factor) - Revenue に寄与する要因を特定する顧客分析システムの実装テンプレート

- [Demand Forecasting (Many Models) Solution Accelerator](https://github.com/microsoft/solution-accelerator-many-models) ([日本語訳](https://github.com/c-nova/solution-accelerator-many-models)) - 大量のモデル構築・推論の実装テンプレート

- [Databricks Solution Accelerators](https://databricks.com/solutions/accelerators) - Databricks 社が提供するユースケースごとの Solution Accelerators


## Recipes
- [Computer Vision](https://github.com/microsoft/computervision-recipes) - コンピュータービジョンのサンプル集

- [Natural Language Processing](https://github.com/microsoft/nlp-recipes) - 自然言語処理 NLP のサンプル集

- [Recommenders](https://github.com/microsoft/recommenders) - 協調フィルタリングなどの推薦アルゴリズム実装サンプル集

- [Forecasting](https://github.com/microsoft/forecasting) - 時系列予測のサンプル集 (ARIMA, LightGBM, Prophet, DilatedCNN etc)

- [MLOps](https://github.com/microsoft/MLOps) - MLOps のベストプラクティス集


<br>

## Usecase


|ユースケース         |ソリューション      |サンプルコード  |
|------------------|------------------|---------|
| Computer Vision   | 医療画像の分類、セグメンテーション | [Project InnerEye](https://github.com/microsoft/InnerEye-DeepLearning)|
||地震層相画像のセグメンテーション| [Deep Seismic](https://github.com/microsoft/seismic-deeplearning)|
||行動認識、人数カウンティング、トラッキング| [Computer Vision Receips](https://github.com/microsoft/computervision-recipes)|
|Personalize        |商品のレコメンデーション|[Azure Synapse Solution Accelerator Retail Recommender](https://github.com/microsoft/Azure-Synapse-Retail-Recommender-Solution-Accelerator)|
||協調フィルタリング、コンテンツベースフィルタリング、ハイブリッド| [Microsoft Recommenders](https://github.com/microsoft/computervision-recipes)([日本語訳](https://github.com/c-nova/recommenders)) |
|Predictive Maintenance     |設備故障 (設備耐用年数) の予測     | - [DeepLearning-Workshop](https://github.com/konabuta/DeepLearning-Workshop/blob/ff71b9a630fc1691f10bfba420d76ee0b90fa3de/Sample/Keras/Keras-LSTM-PredictiveMaintenance-datastore-Hyperdrive.ipynb) <br> - [Predictive Maintenance for remote field devices hands-on lab step-by-step](https://github.com/microsoft/MCW-Predictive-Maintenance-for-remote-field-devices/blob/master/Hands-on%20lab/HOL%20step-by%20step%20-%20Predictive%20Maintenance%20for%20remote%20field%20devices.md)        |
|Autonomous System  |ビル空調の運転最適化         |[bonsai-simulink](https://github.com/microsoft/bonsai-simulink/tree/main/samples/building_energy_management)         |
||化学プラントにおける製造工程最適化      |[bonsai-simulink](https://github.com/microsoft/bonsai-simulink/tree/main/samples/building_energy_management)         |
|Churn Analysis     |退職予測とモデル解釈         | [Responsible AI Widgets - Samples](https://github.com/microsoft/responsible-ai-widgets/blob/main/notebooks/interpretability-dashboard-employee-attrition.ipynb)        |
|Customer Analytics |差分プライバシーによる合成データを用いた年収予測モデルの開発 | [SmartNoise - Samples](https://github.com/opendp/smartnoise-samples/blob/602ecd926c47b891d91009fe2050645d101ca1a1/data/synthesis/mwem_sample/Adult%20Dataset%20Classification%20(Binary).ipynb) |
||年収予測モデルの開発と公平性の評価と軽減| [Responsible AI Widgets - Samples](https://github.com/microsoft/responsible-ai-widgets/blob/main/notebooks/fairness-dashboard-loan-allocation.ipynb)|
||後方互換性を考慮した年収予測モデルの開発|[Backward Compatibility ML - Samples](https://github.com/microsoft/BackwardCompatibilityML/blob/dev/examples/compatibility-analysis-adult.ipynb)|
||患者のガン診断モデルと影響した変数の抽出|[InterpretML - Samples](https://github.com/interpretml/interpret-community/blob/master/notebooks/explain-binary-classification-local.ipynb)|
|Text Analytics     |Livedoor ニュース記事の分類|[AzureML-NLP (日本語)](https://github.com/konabuta/AzureML-NLP)         |
|Credit Analytics   |住宅ローンの与信モデル構築と反実仮想サンプルの生成 | :runner: under construction ([DiCE](https://github.com/interpretml/DiCE)をベースに作成中)         |
|Demand Forecasting |時系列予測 (統計手法、機械学習、深層学習)|[Forecasting Best Practices](https://github.com/microsoft/forecasting)|
||各商品ブランドの店舗ごとの大量モデル開発と推論| [Many Models Solution Accelerator](https://github.com/microsoft/solution-accelerator-many-models)|
|Anomaly Detection  |ビデオの異常検知 (教師あり、教師なし)         | [MLOps_VideoAnomalyDetection](https://github.com/microsoft/MLOps_VideoAnomalyDetection)        |
||不正アクセス検知|[MMLSpark](https://github.com/Azure/mmlspark/blob/master/notebooks/samples/CyberML%20-%20Anomalous%20Access%20Detection.ipynb)|
|Edge AI| エッジデバイスにおける画像認識|[Factory AI Vision](https://github.com/Azure-Samples/azure-intelligent-edge-patterns/tree/master/factory-ai-vision#custom-vision--azure-iot-edge-for-factory-ai) - ONNX with OpenVINO, Nvidia GPU and Arm64 GPU|

<br>


## Tutorial & Workshop

- [Hybrid machine learning](hhttps://github.com/konabuta/azureml-hybrid) - Azure Machine Learning をローカル環境とクラウド環境での学習・推論ハンズオン

- [MLOps on Azure Machine Learning](https://github.com/konabuta/azureml-mlops) - `MLOps` ハンズオンコンテンツ (Github Actions & Azure Pipelines 連携)

- [AutoML Pipeline on Azure Machine Learning](https://github.com/konabuta/AutoML-Pipeline) -  `自動機械学習 AutoML パイプライン`のエンドツーエンド (学習 ~ 推論) のサンプルコード

- [Azure Machine Learning Bootcamp
](https://github.com/konabuta/AzureML-Bootcamp) - Azure Machine Learning Bootcamp (2020年4月 実施)

- [Nvidia Rapids on Azure ML](https://github.com/rapidsai/notebooks-contrib/tree/branch-0.12/conference_notebooks/KDD_2019) - Azure Machine Learning 上で `Nvidia Rapids` を利用するためのチュートリアル。詳細ブログは[こちら](https://medium.com/rapids-ai/rapids-on-microsoft-azure-machine-learning-b51d5d5fde2b)。

- [Azure Machine Learningを使用した PyTorch モデルの分散深層学習](https://github.com/shohei1029/azureml_distributed-pytorch) - `DistributedDataParallel` による分散学習から API 推論まで

- [PyTorch Lightning on Azure Machine Learning](https://github.com/ShuntaIto/azureml-pl-sample) - `PyTorch Lightning` を用いたモデル学習と推論のサンプルコード。`日本語 BERT` の分散学習の実装など。

- [Responsible AI Workshop](https://github.com/konabuta/responsible-ai) - モデル解釈・説明性のテクノジーについてのワークショップコンテンツ。`Explainable Boosting Machine` と `SHAP` の実装。

- [Azure Machine Learning Workshop 2021](https://github.com/konabuta/azureml-workshop-2021) - Azure Machine Learning 4 days ワークショップ

- [ONNX Runtime for model training](https://github.com/microsoft/onnxruntime-training-examples) - ONNX Runtime を用いた Transformer モデル学習の高速化サンプル


<br>

## その他
- [Microsoft Japan Code Labs](https://microsoft.github.io/code-labs-jp/) - ハンズオンコンテンツ (日本マイクロソフトが収集)。AI や Analytics のカテゴリでフィルタリングできます。
- [Azure Samples (GitHub)](https://github.com/Azure-Samples) - Azure のサンプルコード集


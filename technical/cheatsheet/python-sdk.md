## Azure ML Python SDK

### Setup
#### ワークスペースへの接続

```python
from azureml.core import Workspace
ws = Workspace.from_config()
```


### Data
#### Tabular Dataset の作成
##### ローカルからのアップロード
**Upload to datastore**
ローカルから `./data` にデータをアップロードをする。

```python
datastore = ws.get_default_datastore()
datastore.upload(src_dir='./data', target_path='<path/on/datastore>', overwrite=True)
```

**datastore から dataset を作る**
datastore の `<path/o/datastore>` にアップロードされている区切りテキストファイルを利用して dataset を作成する。

```python
datastore = ws.get_default_datastore()
dataset = Dataset.Tabular.from_delimited_files(path = [(datastore, '<path/on/datastore>')])

```
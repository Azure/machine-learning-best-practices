# Conda 仮想環境のセットアップ


### パラメータ
```bash
# For example
export name="myazureml"
export yml_file_path="myazureml.yml"
```

### 新しい conda 仮想環境の作成
```bash
conda env create -n $name -f $yml_file_path
```

### conda 仮想環境の有効化
```bash
conda activate $name
```

### conda 仮想環境の有効化
```bash
ipython kernel install --user --name=$name --display-name=$name
```

### 既存 conda 仮想環境の作成
```bash
conda evn update -n $name -f lightgbm.yml
```


### test

```python
import torch
print("aaa)
```
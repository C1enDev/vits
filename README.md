# 如何使用
需要 Python 大于等于 3.7
## Clone 仓库
```sh
git clone https://github.com/C1enDev/vits.git
```
## 选择 cleaners
- Fill "text_cleaners" in config.json
- Edit text/symbols.py
- Remove unnecessary imports from text/cleaners.py
## 安装依赖
```sh
pip install -r requirements.txt
```
## 创建数据集
### 单人说话
"n_speakers" 在config.json变为0
```
path/to/XXX.wav|transcript
```
- 例子
```
dataset/001.wav|こんにちは。
```
### 多人说话
说话人的ID从0开始
```
path/to/XXX.wav|speaker id|transcript
```
- 例子
```
dataset/001.wav|0|こんにちは。
```
## 预处理
如果已执行cleaned_text，请在 config.json修改
```sh
# 单人 speaker
python preprocess.py --text_index 1 --filelists path/to/filelist_train.txt path/to/filelist_val.txt

# 多人 speakers
python preprocess.py --text_index 2 --filelists path/to/filelist_train.txt path/to/filelist_val.txt
```
## 单调对齐搜索的构建
```sh
cd monotonic_align
python setup.py build_ext --inplace
cd ..
```
## 训练
```sh
# 单人 speaker
python train.py -c <config> -m <folder>

# 多人 speakers
python train_ms.py -c <config> -m <folder>
```
## 推理
### 在线
请看 [inference.ipynb](inference.ipynb)
# 在Docker中使用

```sh
docker run -itd --gpus all --name "Container name" -e NVIDIA_DRIVER_CAPABILITIES=compute,utility -e NVIDIA_VISIBLE_DEVICES=all "Image name"
```


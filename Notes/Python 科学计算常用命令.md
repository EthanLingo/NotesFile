




tags: #日期/2023-10-12 #类型/笔记 

# 镜像源

## 清华镜像源
https://pypi.tuna.tsinghua.edu.cn/simple


# 安装包指令


### PyTorch
#### Windows pip

```shell
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
```


#### Windows conda

```shell
conda install pytorch torchvision torchaudio pytorch-cuda=12.1 -c pytorch -c nvidia
```

#### MacOS

```shell
# MPS acceleration is available on MacOS 12.3+
pip3 install torch torchvision torchaudio
```
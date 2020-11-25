# python-env-setting
## 安装cuda
#### 查看显卡驱动

```bash
cat /proc/driver/nvidia/version
```

![avatar](https://github.com/luckysheep861/python-env-setting/blob/main/pictures/2020-11-24%20at%206.16%20PM.png)

根据显卡驱动选择想安装的cuda版本

![b7cb5a8add8257a063987469affa90ee](https://github.com/luckysheep861/python-env-setting/blob/main/pictures/BFE3F2B9-0A9A-4924-BF57-E35B9BD21F96.png)

#### 下载CUDA Toolkit
[下载地址](https://developer.nvidia.com/cuda-toolkit-archive)
hostnamectl 查看Architecture, Distribution, Version

![228856ac472295acbf19fa5e053422ee](https://github.com/luckysheep861/python-env-setting/blob/main/pictures/2020-11-24%20at%206.26%20PM.png)

Installer Type选择runfile(local)

![fbde1b8eaffc369f8fee6d590da71140](https://github.com/luckysheep861/python-env-setting/blob/main/pictures/2020-11-24%20at%206.19%20PM.png)

#### 安装
```bash
bash cuda_9.2.148_396.37_linux.run
# ..一堆协议说明...
# 按q退出协议说明.
Do you accept the previously read EULA?
accept/decline/quit: accept # 输入accept接受协议

Install NVIDIA Accelerated Graphics Driver for Linux-x86_64 396.37?
(y)es/(n)o/(q)uit: n # 输入n不安装驱动

Install the CUDA 9.2 Toolkit?
(y)es/(n)o/(q)uit: y # 是否安装工具包，选择y

Enter Toolkit Location
 [ default is /usr/local/cuda-9.2 ]: /home/hxtang/.local/env/ # 输入安装地址

Do you want to install a symbolic link at /usr/local/cuda?
(y)es/(n)o/(q)uit: n # 输入n不添加链接

Install the CUDA 8.0 Samples?
(y)es/(n)o/(q)uit: y # 输入n不安装样例
```

#### 下载cuDNN
随便选择一个与刚才下载的CUDA版本对应的cuDNN版本 [下载地址](https://developer.nvidia.com/rdp/cudnn-archive)
解压，与安装的CUDA整合
```bash
tar -zxvf cudnn-9.2-linux-x64-v7.6.5.32.tgz
cp cuda/include/cudnn.h /home/hxtang/.local/env/cuda-9.2/include/  
cp cuda/lib64/libcudnn* /home/hxtang/.local/env/cuda-9.2/lib64
chmod a+r /home/hxtang/.local/env/cuda-9.2/include/cudnn.h /home/hxtang/.local/env/cuda-9.2/lib64/libcudnn*
```


#### 检查
```bash
/home/hxtang/.local/env/cuda-9.2/bin/nvcc
```
![f3044701ac464c68ce43a927b8617db1](https://github.com/luckysheep861/python-env-setting/blob/main/pictures/2020-11-25%20at%209.29%20AM.png)

## 安装python
在python官网下载需要的python source code [下载地址](https://www.python.org/downloads/)
CentOS可用 xz compressed source tarball, 其余使用Gzipped source tarball
![1a471164f76387a7b424adbfd9545c29](https://github.com/luckysheep861/python-env-setting/blob/main/pictures/2020-11-24%20at%206.33%20PM.png)
解压并安装，注意prefix指定需要安装到的目录地址

```bash
tar -xvJf Python-3.6.12.tar.xz
cd Python-3.6.12
./configure --prefix /home/hxtang/.local/env/ --with-ssl
make
make install
```

## 安装pytorch
根据CUDA版本与python版本下载对应的pytorch whl文件，使用安装的python对应的pip安装 [下载地址](https://pytorch.org/get-started/previous-versions/)
```bash
wget cu92/torch-1.5.0%2Bcu92-cp36-cp36m-linux_x86_64.whl
/home/hxtang/.local/env/bin/python3 -m pip install --upgrade pip
/home/hxtang/.local/env/bin/python3 -m pip install torch-1.5.0+cu92-cp36-cp36m-linux_x86_64.whl
```

#### 检查
```
/home/hxtang/.local/env/bin/python3
```
![ce991ec80b79731ace5762293acd4028](https://github.com/luckysheep861/python-env-setting/blob/main/pictures/2020-11-25%20at%209.30%20AM.png)


## 配置环境变量
```bash
export PATH=/home/hxtang/.local/env/bin:$PATH
export PATH=/home/hxtang/.local/env/cuda-9.2/bin:$PATH
export LD_LIBRARY_PATH=/home/hxtang/.local/env/cuda-9.2/lib64:$PATH
```


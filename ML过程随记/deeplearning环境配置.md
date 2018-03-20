# Pycharm + Docker 打造一站式深度学习环境体验
## 缘由
在学习深度学习的过程中，难免会遇到自身电脑硬件配置不够，而实验室拥有高性能服务器的情况，如何能够便捷的将自己的代码和运行所需要的环境分离就成了一个非常重要的问题，于是就有了这篇文章，记录我在配置远程深度学习过程中的一些配置流程和方法。

### 想要达到的目标
* 可以在本地的(自己的台式机或者是笔记本)上编辑深度学习的代码

* 在一个拥有强大显卡的远程机器上训练我的模型

* 在我实时运行的过程中将服务器产生的结果和内容实时的反馈给我的笔记本

## 配置流程
`step.1` 配置带NVIDIA—Docker的docker运行环境

`step.2` 构建自己的深度学习docker image

`step.3` 构建相应的docker-compose来简单目录的挂载和端口的控制

`step.4` 在本地的Pycharm中配置远程的Python interpreter来运行代码

### step.1 
#### 配置docker运行环境
安装docker-ce:

参考： https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-docker-ce-1

`注意：` 在使用docker命令是为了避免需要过高权限的问题(实验室的远程机器上无法拥有sudo权限)，可以采取以下操作来在普通用户环境下使用docker
1. 使用带sudo权限的账号登录系统

2. 创建docker用户分组，并将相应的用户添加到这个分组里
```Bash
sudo groupadd docker
sudo usermod -aG docker your_username
```

3. 退出所有账号，重新登录，使修改生效  

参考： https://docs.docker.com/install/linux/linux-postinstall/

#### 配置nvidia-docker 
1. 各种linux环境下可以直接用yum或者是apt-get安装

2. 为了能连上docker需要对运行环境进行配置
```Bash
vi /etc/docker/daemon.json
```
在文件中加入NVIDIA运行环境的runtimes
```
{
    "runtimes":{
        "nvidia":{
            "path":"/usr/bin/nvidia-container-runtime",
            "runtimeArgs": []
        }
    }
}
```
```Bash
sudo pkill -SIGHUP dockerd
```
3. 尝试使用nvidia-docker查看系统显卡信息
```Bash
nvidia-docker run --rm nvidia/cuda nvidia-smi
```

参考：https://github.com/nvidia/nvidia-container-runtime#docker-engine-setup

### step.2
#### Tips:
我构建了包含TensorFlow，caffe，pytourch等深度学习环境的GPU版可以通过dockerhub查看[DeepLearning Image](https://hub.docker.com/r/zer0like/deeplearning/)具体安装的版本细节请看我的gitHub上的[Dockerfile](https://github.com/zer01ike/Writing/blob/master/ML%E8%BF%87%E7%A8%8B%E9%9A%8F%E8%AE%B0/Dockerfile)

#### 手动构建自己的image
通过docker提供的dockerfile的生成方式，构建自己的深度学习docker环境

本节dockerfile在[floydhub](https://github.com/floydhub/dl-docker/blob/master/Dockerfile.gpu)的GPU上修改而成，主要修改的地方为添加了国内的源和更新了几个插件，和开启了ssh以及sftp方便pycharm的ssh远程管理和远程deployment，


此处需要添加DockerFile的作用以及如何构建的过程



#### build image
```bash
docker build -t "xxx/xxx" . #将当前目录下的DockerFile生成为镜像
```

#### run imgage
当构建好一个nvidia-docker 驱动的image之后可以尝试启动，检查是否出现问题

```bash
nvidia-docker run -d -p 202:22 "xxx/xxx"  /usr/sbin/sshd -D 
#启动ssh 方便链接进去查看是否能够使用Python以及需要的caffe以及TensorFlow环境 
```

利用ssh方式链接进入镜像然后测试tensorflow
```bash
ssh root@0.0.0.0 -p 202
yes
root
python 
import tensorflow
eixt()
```
### step.3
由于每次都需要使用nvida-docker来启动镜像，非常的繁琐和难记，尤其是需要多个端口挂载或者是文件挂载时。
所以我们采用`docker-compose`来简单化启动和运行，节约时间

#### 什么是docker-compose

#### 构建docker-compose前需要注意的事情

#### 如何构建docker-compose

#### 利用docker-compose

### step.4 

#### 配置远程Python环境

#### 配置远程deployment

#### 运行你的tensorflow代码


## 总结
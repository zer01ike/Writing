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


## 总结
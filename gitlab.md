# VR715 gitlab 安装配置和使用说明

## 引子
为满足实验室同学们在代码管理，文档版本管理和中心存储方面的问题，我和晓川师兄商量去部署一个实验室内部的版本管理系统。现详细说明其在安装，部署和使用过程中的注意事项。

## 安装规划
在实验室的大服务器上采用docker虚拟化技术搭建服务网站，确保不影响各位师兄师姐的实验环境，重新开启一个名为gitlab的账户，专用服务于网站系统

### 重要参数
`usrname`: gitlab `password`:git@vr715

## 部署方案

由于采用的是docker的轻量级快速部署方案，利用已有的docker image即可快速部署服务环境。具体采用的image和各种参数如下表所示：
image: twang2218/gitlab-ce-zh:10.5.1 为gitlab的中文社区版
端口映射：80:80 宿主机的80口映射为镜像的80口
        443:443 宿主机的443口映射为镜像的443口
        2222:22 宿主机的2222口映射为镜像的22口，由于宿主机的22口常默认用来连接SSH，为防止冲突采用2222口
文件挂载位置：
        /home/gitlab/gitlab_volumes/config config文件挂载位置
        /home/gitlab/gitlab_volumes/data data文件挂载位置
        /home/gitlab/gitlab_volumes/logs log文件挂载位置

### 备份和恢复方案
利用docker attach 进入镜像，采用常用的备份方案进行备份

## 使用

### 常规使用

### 配置内网远程库



# LinuxCommand

Some command line commands in Linux

sudo vim /etc/apt/sources.list

 apt-get update
 apt-get upgrade apt-get install <packagename>
 apt get install aptitude 

#共享剪贴板
sudo apt update # 首先要更新，保证apt库是最新的
sudo apt install open-vm-tools
sudo apt install open-vm-tools-desktop
vmware-user # 直接运行即可，open-vm-tools给你内置了


sudo  cp   /etc/apt/sources.list   /etc/apt/sources.list.bak

sudo vim /etc/apt/sources.list

```# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ groovy main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ groovy main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ groovy-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ groovy-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ groovy-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ groovy-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ groovy-security main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ groovy-security main restricted universe multiverse

# 预发布软件源，不建议启用
# deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ groovy-proposed main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ groovy-proposed main restricted universe multiverse
```


--我的配置--
deb http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
 
deb http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse
 
deb http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse
 
deb http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse




在Ubuntu系统上安装Docker，可以按照以下步骤操作：

更新软件包索引：

sudo apt-get update

允许APT使用HTTPS：

sudo apt-get install apt-transport-https ca-certificates curl software-properties-common

添加Docker官方GPG密钥：

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

添加Docker的稳定版本仓库：

sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

再次更新软件包索引：

sudo apt-get update

安装Docker CE（社区版）：

sudo apt-get install docker-ce
sudo apt-get install docker.io

验证Docker是否安装成功并运行：

sudo systemctl status docker

或者简单地运行：

sudo docker run hello-world

如果安装成功，你将看到Docker拉取hello-world镜像并运行容器的信息。



------------------安装ssh服务-----------------------
在Ubuntu上安装SSH服务，您可以按照以下步骤操作：

更新包列表：

sudo apt update

安装OpenSSH服务器软件包：

sudo apt install openssh-server

安装完成后，SSH服务将自动启动。您可以使用以下命令检查SSH服务的状态：

sudo systemctl status ssh

如果SSH服务没有自动启动，您可以使用以下命令启动它：

sudo systemctl start ssh

为了确保SSH服务在系统启动时自动启动，可以使用以下命令：

sudo systemctl enable ssh

（可选）如果您需要修改SSH配置，编辑 /etc/ssh/sshd_config 文件，然后重启SSH服务以应用更改：

sudo systemctl restart ssh

确保您的防火墙允许SSH连接。如果您使用的是UFW，可以使用以下命令允许SSH连接：

sudo ufw allow ssh

现在，您应该可以从远程客户端使用SSH连接到您的Ubuntu服务器了。使用以下命令进行连接：

ssh [username]@[server-ip-address]

其中 [username] 是您的Ubuntu服务器上的用户名，[server-ip-address] 是服务器的IP地址。

sudo apt install aptitude 


解决方法


这是因为,openssh-server是依赖于openssh-clien的,ubuntu自带的openssh-clien与所要安装的openssh-server所依赖的版本不同,这里所依赖的版本是 1:8.2p1-4

所以要安装对应版本的openssh-clien,来覆盖掉ubuntu自带的

执行下面命令：

sudo apt-get install openssh-client=1:8.2p1-4
安装完对应版本的openssh-clien后再执行：

sudo apt-get install openssh-server

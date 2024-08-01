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




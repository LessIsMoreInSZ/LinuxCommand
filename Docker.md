在Ubuntu系统上安装Docker，可以按照以下步骤操作：

更新软件包索引：

sudo apt-get update

允许APT使用HTTPS：

sudo apt-get install apt-transport-https ca-certificates curl software-properties-common

添加Docker官方GPG密钥（可选，20.04后不输入此命令）：

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

## 20.04后输入此命令

运行以下命令时：

bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
如果出现错误或警告，可能是因为 apt-key 在较新的 Ubuntu 版本（如 20.04 及更高版本）中已被弃用，或者你的系统缺少必要的工具。以下是解决方法和建议。

1. ​检查 curl 是否安装
确保系统中已安装 curl，如果没有安装，可以运行以下命令安装：

bash
sudo apt update
sudo apt install curl -y
2. ​检查 apt-key 是否可用
在 Ubuntu 20.04 及更高版本中，apt-key 已被弃用，建议使用其他方法来管理 GPG 密钥。

如果你仍然想使用 apt-key，可以尝试以下命令，但请注意，这可能会在未来版本的 Ubuntu 中失效：

bash
sudo apt-key add -
3. ​推荐方法：将密钥添加到特定目录
从 Ubuntu 20.04 开始，推荐将 GPG 密钥添加到 /etc/apt/keyrings/ 目录中，而不是使用 apt-key。

运行以下命令：

bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
这会将 Docker 的 GPG 密钥保存为 /usr/share/keyrings/docker-archive-keyring.gpg，并以 gpg 格式存储。
4. ​更新 Docker 的软件源
接下来，添加 Docker 的官方软件源。运行以下命令：

对于 Ubuntu 20.04 (Focal) 或更高版本：
bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
$(lsb_release -cs) 会自动检测你的 Ubuntu 版本代号（如 focal、jammy 等）。
signed-by=/usr/share/keyrings/docker-archive-keyring.gpg 指定了 GPG 密钥的位置。
5. ​更新软件包列表
添加 Docker 的软件源后，更新软件包列表：

bash
sudo apt update
6. ​安装 Docker
现在可以安装 Docker 了。运行以下命令：

bash
sudo apt install docker-ce docker-ce-cli containerd.io -y
7. ​验证 Docker 是否安装成功
安装完成后，运行以下命令验证 Docker 是否正常工作：

bash
sudo docker run hello-world
如果看到类似以下的输出，说明 Docker 安装成功：

Hello from Docker!
This message shows that your installation appears to be working correctly.
##
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


--




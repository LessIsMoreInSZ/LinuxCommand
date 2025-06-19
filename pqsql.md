一、Ubuntu/Debian 系统安装
步骤1：添加官方仓库并安装
bash
# 创建仓库配置文件
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'

# 导入签名密钥
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -

# 更新并安装
sudo apt update
sudo apt install postgresql postgresql-contrib
步骤2：验证安装
bash
# 检查服务状态
sudo systemctl status postgresql

# 查看版本
sudo -u postgres psql -c "SELECT version();"
二、CentOS/RHEL 系统安装
步骤1：添加官方仓库
bash
# CentOS 7/8
sudo yum install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm

# CentOS 9/RHEL 9
sudo dnf install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-9-x86_64/pgdg-redhat-repo-latest.noarch.rpm
步骤2：安装PostgreSQL
bash
# CentOS 7/8
sudo yum install -y postgresql16-server

# CentOS 9/RHEL 9
sudo dnf install -y postgresql16-server
步骤3：初始化并启动
bash
# 初始化数据库
sudo /usr/pgsql-16/bin/postgresql-16-setup initdb

# 启动服务
sudo systemctl enable postgresql-16
sudo systemctl start postgresql-16
三、基础配置
1. 修改管理员密码
bash
sudo -u postgres psql
\password postgres  # 设置新密码
\q
2. 启用远程访问
修改配置文件：

bash
sudo nano /var/lib/pgsql/16/data/postgresql.conf
取消注释并修改：

conf
listen_addresses = '*'   # 允许所有IP连接
port = 5432              # 默认端口
修改访问控制：

bash
sudo nano /var/lib/pgsql/16/data/pg_hba.conf
在文件末尾添加：

conf
# 允许所有IP通过密码访问
host    all             all             0.0.0.0/0               md5
3. 重启服务应用配置
bash
sudo systemctl restart postgresql-16
四、防火墙配置
bash
# Ubuntu
sudo ufw allow 5432

# CentOS/RHEL
sudo firewall-cmd --permanent --add-port=5432/tcp
sudo firewall-cmd --reload
五、常用操作命令
操作	命令
启动服务	sudo systemctl start postgresql
停止服务	sudo systemctl stop postgresql
进入交互终端	sudo -u postgres psql
创建新用户	CREATE USER demo WITH PASSWORD 'password123';
创建数据库	CREATE DATABASE mydb OWNER demo;
备份数据库	pg_dump -U postgres mydb > mydb_backup.sql
恢复数据库	psql -U postgres mydb < mydb_backup.sql
六、安装扩展（如PostGIS）
bash
# Ubuntu
sudo apt install postgresql-16-postgis-3

# CentOS/RHEL
sudo yum install postgis31_16
在数据库中启用：

sql
CREATE EXTENSION postgis;
常见问题解决
连接被拒绝

检查postgresql.conf中的listen_addresses

检查pg_hba.conf中的访问规则

检查防火墙设置

忘记postgres密码
切换到Linux的postgres用户修改：

bash
sudo su - postgres
psql
ALTER USER postgres WITH PASSWORD 'new_password';
端口冲突
检查端口使用情况：

bash
sudo netstat -tulnp | grep 5432

CentOS中安装Node、MySQL、Apache、VSFTP、MongoDB等软件

### 一、安装及配置Node环境

#### 1、首先安装wget

```
yum install -y wget
```

#### 2、下载nodejs最新的bin包

```
wget https://nodejs.org/dist/v8.11.4/node-v8.11.4-linux-x64.tar.xz
```

#### 3、解压包 

```
xz -d node-v8.11.4-linux-x64.tar.xz
tar -xf node-v8.11.4-linux-x64.tar
```

####4、部署bin文件(配置环境变量)

```
ln -s ~/node-v8.11.4-linux-x64/bin/node /usr/bin/node
ln -s ~/node-v8.11.4-linux-x64/bin/npm /usr/bin/npm
```



###二、安装MySQL及配置环境变量

#### 1、下载并安装MySQL官方的 Yum Repository

```
# 安装用的Yum Repository
wget -i -c http://dev.mysql.com/get/mysql57-community-release-el7-10.noarch.rpm

# 直接yum安装
yum -y install mysql57-community-release-el7-10.noarch.rpm

# 开始安装MySQL服务器
yum -y install mysql-community-server
```

#### 2、MySQL数据库设置

```
# 首先启动MySQL
systemctl start mysqld.service

# 查看MySQL运行状态
systemctl status mysqld.service

# 此时MySQL已经开始正常运行，不过要想进入MySQL还得先找出此时root用户的密码，通过如下命令可以在日志文件中找出密码
grep "password" /var/log/mysqld.log

# 进入数据库
mysql -u root -p

# 新密码设置的时候如果设置的过于简单会报错，可以通过如下指令更改密码策略，再设置密码
set global validate_password_policy=0;
set global validate_password_length=1;

# 输入初始密码，此时不能做任何事情，因为MySQL默认必须修改密码之后才能操作数据库
ALTER USER 'root'@'localhost' IDENTIFIED BY 'new password';

# 此时还有一个问题，就是因为安装了Yum Repository，以后每次yum操作都会自动更新，需要把这个卸载掉
yum -y remove mysql57-community-release-el7-10.noarch
```

#### 3、开启远程连接

```
# 在云主机上连接mysql
mysql -u root -p #根据提示输入密码

# 依次执行以下sql命令
use mysql; #打开 mysql 数据库

# 将host设置为%表示任何ip都能连接mysql，当然也可指定为某个特定ip
update user set host='%' where user='root' and host='localhost';
flush privileges; #刷新权限表，使配置生效

# 接下来就可以在windows上面使用图形化工具连接了
```



### 三、安装Apache及配置环境变量

#### 1、安装Apache服务程序(apache服务的软件包名称叫做httpd)

```javascript
yum install httpd -y
```

#### 2、对Apache服务操作的一些指令

```
# 启动Apache服务
systemctl start httpd.service

# 关闭Apache服务【暂时不需要执行】
systemctl stop httpd.service

# 重启Apache服务【暂时不需要执行】
systemctl restart httpd.service

# 查看Apache服务状态【暂时不需要执行】
systemctl status httpd.service

# 把Apache服务做成开机自动启动
systemctl enable httpd.service
```

#### 3、更改Apache默认配置

```
# 首先在项目根目录创建一个ftp/WWW文件夹
cd /
mkdir ftp
mkdir WWW

# 编辑默认配置
sudo vim /etc/httpd/conf/httpd.conf

# 更改站点根目录
修改地方1： DocumentRoot "/var/www/html" 改成 DocumentRoot "/ftp/WWW"
修改地方2： <Directory "/var/www/html"> 改成 <Directory "/ftp/WWW">
```

### 四、安装VSFTP及配置

#### 1、安装VSFTP

```
# 安装
yum install vsftpd
```

#### 2、配置VSFTP

```
# 打开配置
vim /etc/vsftpd/vsftpd.conf

# 更改配置
把 anonymous_enable=YES 设置为 anonymous_enable=NO 不允许匿名登录FTP

# 下面的可以暂时不执行
vi /etc/ssh/sshd_config 
将Subsystem      sftp    /usr/libexec/openssh/sftp-server 
 
改为Subsystem       sftp    internal-sftp 
```

#### 3、对VSFTP服务的各种操作

```
# 启动VSFTP服务
systemctl start vsftpd.service

# 停止VSFTP服务【暂时不需要执行】
systemctl stop vsftpd.service

# 重启VSFTP服务【暂时不需要执行】
systemctl restart vsftpd.service

# 查看VSFTP状态【暂时不需要执行】
systemctl status vsftpd.service

# 开机自动启动VSFTP服务
systemctl enable vsftpd.service

# 取消开机自动启动VSFTP服务【暂时不需要执行】
systemctl disable vsftpd.service
```

#### 4、创建VSFTP用户及设置权限

```
# 创建用户 /sbin/nologin：不允许此用户登录系统，但可以登录FTP
useradd -d /ftp/WWW -s /sbin/nologin 你登录FTP的用户名

# 设置用户密码 回车，输入密码即可（需输入两次）
passwd 你登录FTP的用户名

# 检查是否设置成功
cat /etc/passwd 
```

### 五、安装MongoDB及配置

#### 1、下载及安装

```
# 下载
wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-rhel70-4.0.1.tgz

# 解压
tar -zxvf mongodb-linux-x86_64-rhel70-4.0.1.tgz

# 重命名
mv mongodb-linux-x86_64-rhel70-4.0.1 mongodb
```

#### 2、启动及配置 MongoDB

```
# 移动到 /usr/local目录下
mv mongodb /usr/local

# 设置环境变量 打开profile
vim  /etc/profile

# 在 export PATH USER LOGNAME MAIL HOSTNAME HISTSIZE HISTCONTROL 上面添加下面命令
 export PATH=/usr/local/mongodb/bin:$PATH
 
# 按esc 退出编辑 ，按 shift + : 输入wq保存
 
# 验证 
输入 mongo 出现版本号，表示配置成功 

```

#### 3、设置成开机启动

```
# 在mongodb的bin目录下创建mongodb.conf，并且写上脚本
touch mongodb.conf

写上下面的内容

dbpath=/home/data/db
logpath=/home/data/logs/mongodb.log
logappend=true
port=27017


```



### 六、Nginx的安装及配置

####1、下载及安装

```
# 下载压缩包
wget http://nginx.org/download/nginx-1.14.1.tar.gz

# 解压
tar -xzf nginx-1.14.1.tar.gz
```

#### 2、Nginx的相关配置

```
# 拷贝nginx中的vim文件
cp -r contrib/vim/* ~/.vim/
```

#### 3、编译Nginx

```
参考:
	https://www.cnblogs.com/jerrypro/p/7062101.html
	
# 首先由于nginx的一些模块依赖一些lib库，所以在安装nginx之前，必须先安装这些lib库，这些依赖库主要有g++、gcc、openssl-devel、pcre-devel和zlib-devel 所以执行如下命令安装
	 yum install gcc-c++  
     yum install pcre pcre-devel  
     yum install zlib zlib-devel  
     yum install openssl openssl--devel  

# 查看配置文件支持的参数
./configure --help | more

# 编译到指定目录(这个就是Nginx的安装目录)
./configure --prefix=/ftp/nginx

	如果出现错误:
		需要安装pcre库哦。如果是centos，请使用yum install pcre pcre-devel -y命令安装

# 编译nginx
make

# 安装
make install

# 检查nginx安装的目录
whereis nginx  
```








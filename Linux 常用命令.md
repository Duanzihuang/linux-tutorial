## Linux 常用命令

### 一、文件及文件夹操作

```
# 创建文件夹
mkdir 文件夹名称

# 删除文件夹
rm -f 文件夹名称

# 重命名文件夹
mv 旧文件夹名 新文件夹名

# 解压文件
tar -xf node-v8.11.4-linux-x64.tar

# 解压zip包(需要安装zip/unzip  yum -y install zip)
unzip mydata.zip -d mydatabak
```

### 二、执行文件操作

```
# 创建快捷方式（以node为例）
ln -s ~/node-v8.11.4-linux-x64/bin/node /usr/bin/node

# 查找文件所在位置
whereis nginx.conf

# 拷贝文件
cp 源文件(source) 目标文件(destination)

# 移动文件
mv source destination

# 删除文件
rm -rf 文件名称

# 更改文件 & 文件夹权限
chmod 777 文件&文件夹名
```

### 三、创建服务

```
# 创建类似于httpd.service的服务
vi /lib/systemd/system/mongodb.service
```


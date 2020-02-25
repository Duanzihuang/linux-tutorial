## 基本概念

> 什么是Docker 详细解释可以参考：https://my.oschina.net/jamesview/blog/2994112

```
它是一个容器，把我们的代码、运行环境、配置文件、依赖的包等等，打包成为一个镜像，达到能快速移植的目的。

docker是一个开源的软件部署解决方案；
docker也是轻量级的应用容器框架；
docker可以打包、发布、运行任何的应用。

核心思想：镜像(image)、容器(container)、仓库(repository)
  			镜像：类
  			容器：对象，在容器中运行我们的App
  			仓库：集中存放镜像文件的场所
  			
关系：有镜像才能创建出容器

方便理解：高度浓缩版/袖珍版的Linux（除去了模拟硬件等一系列操作）
```

> 为什么要有Docker

```
如果没有Docker，那么运维工程师的工作将非常的繁杂，特别是遇到集群部署的时候会非常痛苦。
除开操作系统不一样之外（可能开的同学用的是Window、Mac系统，运维同学用的是Linux系统），当进行集群部署的时候（部署很多台机器），使用传统的模式，运维同学得一台一台的安装所需要的环境（比如Tomcat、Nginx、Node、JDK等等）。这样的话工作会很繁琐。
如果使用Docker部署的话，只需要先创建一个Docker镜像，然后再集群部署的时候，把已经创建好的一个Docker镜像（当然里面已经安装好了各种部署需要的软件Tomcat、Node、JDK等），直接拷贝到各个机器上就可以轻松完成各项工作了，并且还可以保证部署的一致性。
```

## 实战操作

> Docker的下载、安装&配置

```
# CentOS 6.x
yum install -y epel-release
yum install -y docker-io
安装后的配置文件：/etc/sysconfig/docker
启动Docker后台服务：service docker start
验证是否OK：docker version

# CentOS 7.x
参考：https://docs.docker.com/install/linux/docker-ce/centos/
sudo yum install docker-ce docker-ce-cli containerd.io 【ce是社区版】
启动Docker后台服务：sudo systemctl start docker / sudo systemctl restart docker
验证是否OK：docker version

# 配置镜像加速
登录阿里云：https://cr.console.aliyun.com/cn-shenzhen/instances/mirrors 获取自己的镜像加速地址
并且选择 CentOS 按照指令进行配置
检测是否配置好了：ps -ef|grep docker

# Hello World

```

> Docker常见命令

```
# 帮助命令
docker version
docker info
docker --help

# 镜像命令
docker images 列出本地的镜像，选项 -a(列出所有) -q(只显示镜像ID) --digests(显示摘要信息) --no-trunc(显示镜像的完整信息)
docker search nginx 选项 -s 30(点赞数大于30的) --no-trunc(显示镜像的完整信息，不要省略)
docker pull nginx 选项 :版本
docker rmi 删除某个镜像 选项 -f(强制删除) 
docker rmi -f $(docker images -qa)

# 容器命令
docker run -it 镜像的id/名字 选项 -i(交互)  -t(伪终端) --name(指定容器的名字) -d(以守护进程方式启动)
docker run -d 镜像的id/名字 以守护进程的方式启动
docker run -d centos /bin/sh -c "while true;do echo hello girl;sleep 2;done"
docker ps 列出当前所有运行的容器进程 选项 -l(查看上一次的容器) -a(所有的) -n 3(上三次显示的) -q(只显示容器编号)
docker stop 容器id
docker kill 容器id
exit : 容器停止退出
ctrl + p + q ：容器不停止退出
docker start 容器id
docker restart 容器id
docker rm 容器id
docker rm -f $(docker ps -aq) 删除全部的容器
docker logs -f -t --tail 容器id
docker top 容器id
docker inspect 容器id 查看容器的信息
docker attach 容器id 重新进入之前停止的容器
docker exec -t 容器id 指令... 重新打开容器并且运行指令
docker cp 容器id:容器内路径 目的主机路径
docker run -it -p 8888:8080 tomcat 开启tomcat容器，tomcat的端口是8080，访问需要使用8888
docker commit -a="作者" -m="注释" 容器id itcast/mytomcat:1.2 根据容器id创建一个新的镜像
```

> Docker 相关概念

```
数据容器卷
	就是实现docker中的数据持久化用的
	作用：容器的持久化、容器间继承 + 共享数据
```

## Docker常用命令

```
docker build

docker pull

docker run
```

## Docker相关命令

```
# 查看当前Linux内核版本
uname -r

# 查看当前Linux的版本
cat /etc/redhat-release

# 查看当前CentOS中的所有进程
ps -ef

# 查看Linux进程
top

# 删除文件
rm -rf 文件名称
```


Docker

## 基本概念

> 什么是Docker

```
它是一个容器，把我们的代码、运行环境、配置文件、依赖的包等等，打包成为一个镜像，达到能快速移植的目的。

docker是一个开源的软件部署解决方案；
docker也是轻量级的应用容器框架；
docker可以打包、发布、运行任何的应用。

核心思想：镜像(image)、容器(container)、仓库(repository)
  			镜像：类
  			容器：对象，在容器中运行我们的App
  			仓库：集中存放镜像文件的场所

方便理解：高度浓缩版/袖珍版的Linux（除去了模拟硬件等一系列操作）
```

> 为什么要有Docker

```
如果没有Docker，那么运维工程师的工作将非常的繁杂，特别是遇到集群部署的时候会非常痛苦。
除开操作系统不一样之外（可能开的同学用的是Window、Mac系统，运维同学用的是Linux系统），当进行集群部署的时候（部署很多台机器），使用传统的模式，运维同学得一台一台的安装所需要的环境（比如Tomcat、Nginx、Node、JDK等等）。这样的话工作会很繁琐。
如果使用Docker部署的话，只需要先创建一个Docker镜像，然后再集群部署的时候，把已经创建好的一个Docker镜像（当然里面已经安装好了各种部署需要的软件Tomcat、Node、JDK等），直接拷贝到各个机器上就可以轻松完成各项工作了，并且还可以保证部署的一致性。
```

## 实战操作

> Docker的下载与安装

```

```

> Docker常见操作

```

```

> Docker Hub

```

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
```


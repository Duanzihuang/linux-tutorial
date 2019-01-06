# 安装软件

## yum
	Yum（全称为 Yellow dog Updater, Modified）是一个在Fedora
	和RedHat以及CentOS中的Shell前端软件包管理器。基于RPM包管
	理，能够从指定的服务器自动下载RPM包并且安装，可以自动处理依
	赖性关系，并且一次安装所有依赖的软件包，无须繁琐地一次次下
	载、安装。
	
	参考:https://baike.baidu.com/item/yum/2835771?fr=aladdin
	
## 安装wget
	wget命令用来从指定的URL下载文件。wget非常稳定，它在带宽很窄
	的情况下和不稳定网络中有很强的适应性，如果是由于网络的原因下
	载失败，wget会不断的尝试，直到整个文件下载完毕。如果是服务器
	打断下载过程，它会再次联到服务器上从停止的地方继续下载。这对
	从那些限定了链接时间的服务器上下载大文件非常有用。
	
	参考:http://man.linuxde.net/wget
	
## 安装NodeJS
	参考:https://blog.csdn.net/xerysherryx/article/details/78920978
	
## 设置npm全局包的环境变量
	http://19911001.iteye.com/blog/2339410
	
## 安装mysql
	https://blog.csdn.net/z13615480737/article/details/78906598
	
## 执行sql语句
	https://blog.csdn.net/cx136295988/article/details/74188447
	
## 安装Apache
	https://blog.csdn.net/Metropolis_cn/article/details/71374594
	
	https://blog.csdn.net/qiandublog/article/details/52505791
	
	开放80端口：
		iptables -I INPUT -p TCP --dport 80 -j ACCEPT
	
	查看Apache状态:
		systemctl status httpd
		
	启动Apache
		systemctl start httpd
	
	重启Apache
		systemctl restart httpd
		
	Apache配置文件所在目录
		/etc/httpd/conf/httpd.conf
		
	Apache访问403错误解决
		https://www.cnblogs.com/starof/p/4685999.html
	
## 安装MongoDB
	https://www.cnblogs.com/web424/p/6928992.html
	
	https://www.cnblogs.com/acewhl/p/6638486.html
	
	mongodb操作
	http://www.cnblogs.com/zhoujinyi/p/4610050.html
	
--------------------------------

# 拷贝代码到CentOS
	
## 搭建FTP服务器并且连接
	https://blog.csdn.net/qq_32786873/article/details/78730303

--------------------------------
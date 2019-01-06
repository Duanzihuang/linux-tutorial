# Linux 之连接到阿里云CentOS服务器

### 使用SSH免密登录

```
# 在自己的Windows或是Mac电脑上生成一对RSA公私钥【参考GitHub生成公私钥】
参考地址:https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/

# 输入如下指令，然后一路回车
ssh-keygen -t rsa -b 4096 -C "your_email@example.com" 

# 将公钥上传到CentOS的 /root/.ssh目录下，可借助FileZilla这个工具

# 将公钥中的内容拷贝到 authorized_keys 里面，如果没有该文件则创建
touch authorized_keys # 如果没有authorized_keys这个文件，则创建
cat id_rsa.pub >> authorized_keys # 把公钥文件(id_rsa.pub)中的内容拷贝到authorized_keys中

# 打开Git Bash，使用如下指令进行免密登录
ssh root@你的阿里云服务器地址

注意：第一次的时候，你还是需要输入密码才能登录的，等配置好了免密登录之后，就可以实现免密登录了
```








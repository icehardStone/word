# `NFS 网路文件系统使用操作手册`

NFS 网络文件系统的使用流程

  >* 服务端启动RPC服务，并开启端口
  >* 启动NFS服务之后并向RPC服务注册端口信息
  >* 客户端启动RPC服务向服务端的RPC服务请求请求服务端的NFS端口，服务端返回NFS的端口信息给客户端。
  >* 客户端通过获取的端口通过和服务端的NFS建立连接。

搭建NFS服务器的作用:

* 节省本地存储空间
* 集中用户管理
* 减少硬件设备的使用
 
安装NFS服务

``` shell
rpm -qa | grep rpcbind
rpm -qa | grep nfs-utils

# yum install -y nfs
```

创建共享目录

``` shell
mkdir /share /common
```

开启服务并查看相关进程和端口

``` shell
systemctl start rpcbind
systemctl start nfs

# 添加开机启动
systemctl enable rpcbind
systemctl enable nfs

# 查看进程
ps -ef | grep rpcbind
ps -ef | grep nfs
netstat -lntup | grep 111
```

编辑NFS的主配置文件

``` shell
vi /etc/exports

# 进入编辑状态，添加相关行记录
/share *(ro)
/common  * (ro)
/common 192.168.1.20/24(rw,all,squash)

## 保存，退出: wq!

# 重新加载配置
exports -v
```

挂载客户端

``` shell
mkdir /mnt/124
mkdir /mnt/456

# 将192.168.1.10 nfs的服务器的 /share 目录挂载到本地 /mnt/124目录
mount -t nfs 192.168.1.10:/share /mnt/124
# 将192.168.1.10 nfs的服务器的 /common目录挂载到本地 /mnt/456目录中去
mount -t nfs 192.168.1.10:/common /mnt/456
```



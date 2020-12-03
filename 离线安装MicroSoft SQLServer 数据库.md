# CentOS 7上离线安装MicroSoft SQLServer 数据库

* 创建目录
* 下载安装包
* 离线安装

## 创建目录

``` shell
mkdir sqlserver2014
```

## 下载安装包

主要目录 https://packages.microsoft.com/rhel/7/

### 下载mssql-server-2017
wget https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm

### 下载 msodbcsql, mssql-tools
wget https://packages.microsoft.com/rhel/7.3/prod/msodbcsql-13.1.6.0-1.x86_64.rpm  
wget https://packages.microsoft.com/rhel/7.3/prod/mssql-tools-14.0.5.0-1.x86_64.rpm

## 下载 sqlserver agent
wget https://packages.microsoft.com/rhel/7/mssql-server/mssql-server-agent-14.0.900.75-1.x86_64.rpm

## 安装

``` shell
rpm -ivh mssql-server-14.0.1000.169-2.x86_64.rpm
/opt/mssql/bin/mssql-conf setup

#需要依赖包:  
    warning: ./temp/mssql-server-14.0.3030.27-1.x86_64.rpm: Header V4 RSA/SHA256 Signature, key ID be1229cf: NOKEY  
    error:sFailed dependencies:  
            bzip2 is needed by mssql-server-14.0.3030.27-1.x86_64  
            gdb is needed by mssql-server-14.0.3030.27-1.x86_64  
            libsss_nss_idmap is needed by mssql-server-14.0.3030.27-1.x86_64  

#设置密码为: hu12345678@  

yum localinstall msodbcsql-13.1.6.0-1.x86_64.rpm  
yum localinstall mssql-tools-14.0.5.0-1.x86_64.rpm
```


配置环境变量:

``` shell
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
source ~/.bash_profile 
echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
source ~/.bashrc
```

开放防火墙端口 1433


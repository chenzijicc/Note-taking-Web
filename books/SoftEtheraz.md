# SoftEther 安装

## Linux安装：
### 1.安装依赖包
```shell
yum -y install make gcc gcc-devel gcc-c++ zlib-devel openssl-devel readline-devel ncurses-devel
```
### 2.解压安装包
```shell
tar -xf softether-vpnserver-v4.38-9760-rtm-2021.08.17-linux-x64-64bit.tar.gz -C /usr/local/
```
### 3.执行安装
```shell
make
```
在安装完成Softether服务后，我们执行命令（在Softether解压后的目录下）：
```shell
./vpnserver start
```

### 4.添加服务
```shell
vim /etc/init.d/vpnserver

#内容如下：
#!/bin/sh
# chkconfig: 2345 99 01
# description: SoftEther VPN Server
DAEMON=/usr/local/vpnserver/vpnserver
LOCK=/var/lock/subsys/vpnserver
test -x $DAEMON || exit 0
case "$1" in
start)
$DAEMON start
touch $LOCK
;;
stop)
$DAEMON stop
rm $LOCK
;;
restart)
$DAEMON stop
sleep 3
$DAEMON start
;;
*)
echo "Usage: $0 {start|stop|restart}"
exit 1
esac
exit 0
```
### 5.添加开机启动
```shell
chmod 755 /etc/init.d/vpnserver
/sbin/chkconfig --add vpnserver
```
### 6.启动服务
```shell
/etc/init.d/vpnserver start
```
### 7.开放端口
UDP端口：4500和500
TCP端口：1194
还需开放SoftEther VPN的server的通信的端口(443和5555)
### 8.进行配置管理
（配置管理直接在客户端安装SoftEther VPN Server，使用服务器ip+端口号进行连接）

## Windows
(windows下直接安装SoftEther VPN Server 安装完全傻瓜化，直接点击下一步，安装完成后进行可视化配置，连接本地ip+端口号)
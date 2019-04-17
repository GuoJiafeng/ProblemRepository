# CentOS 6 环境下配置双网卡



# 网卡1

~~~properties
DEVICE=eth0
TYPE=Ethernet
ONBOOT=yes
NM_CONTROLLED=yes
BOOTPROTO=static
IPADDR=192.168.134.99
NETMASK=255.255.255.0
BROASCAST=192.168.134.255

#解释： 双网卡配置之网卡一   使用只粘贴上方文字
#网卡1使用NAT模式
#静态IP
#网段与自身虚拟机配置保持一致 即可
#作为虚拟机之前通信使用

~~~

# 网卡2

~~~properties
DEVICE=eth1
TYPE=Ethernet
ONBOOT=yes
NM_CONTROLLED=yes
BOOTPROTO=dhcp

#解释： 双网卡配置之网卡二   使用只粘贴上方文字
#网卡1使用桥接模式
#动态IP
#作为连接公网使用
~~~



# 相关命令

~~~sehll
vi /etc/sysconfig/network-scripts/ifcfg-eth0  
rm -rf  /etc/udev/rules.d/70-persistent-net.rules #删除MAC地址
service network restart 
service iptables stop
chkconfig iptables off
~~~














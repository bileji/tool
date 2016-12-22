# 防火墙相关
---
+ **Centos7+ 安装iptables**

	```
	$yum -y install iptables-services
	$systemctl mask firewalld.service
	$systemctl enable iptables.service && systemctl enable ip6tables.service
	$systemctl stop firewalld.service
	$systemctl start iptables.service && systemctl start ip6tables.service
	$ln -s /lib/lsb/init-functions /etc/rc.d/init.d/functions
	```
+ **开启防火墙日志**

	```
	```
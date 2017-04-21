## shadowsocks安装
---
+ 基础环境安装:

```
$yum -y install gcc automake autoconf libtool make m2crypto \
autoconf libtool curl curl-devel zlib-devel openssl-devel \
perl perl-devel cpio expat-devel gettext-devel pcre-devel asciidoc xmlto git
```
+ 克隆shadowsocks-libev

```
$git clone https://github.com/shadowsocks/shadowsocks-libev.git
```
+ 编译安装

```
$cd shadowsocks-libev
$./configure && make && make install
```

+ 启动shadowsocks
	
	+ 服务端

		```
		$echo "alias shadowsocks='ss-server -s your_server_ip -p 8388 -k your_pwd -m aes-256-cfb -t 300 > /dev/null 2>&1 &'" >> ~/.bashrc
		$soure ~/.bashrc && shadowsocks
		```
	+ 客户端
	
		```
		$echo "alias shadowsocks='ss-local -s your_server_ip -p 8388 -l 1080 -m aes-256-cfb -k your_pwd > /dev/null 2>&1 &'" >> ~/.bashrc
		$source ~/.bashrc && shadowsocks
		```

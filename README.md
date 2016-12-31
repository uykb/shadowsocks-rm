shadowsocks
===========

[![PyPI version]][PyPI]
[![Build Status]][Travis CI]

Features:
- TCP & UDP support
- User management API
- TCP Fast Open
- Workers and graceful restart
- Destination IP blacklist

Server
------

### Install

更新系统 
apt-get update && apt-get upgrade -y
安装控件
apt-get install python-pip  && pip install cymysql
安装组建
apt-get install vim git wget supervisor -y
下载shadowsocks-rm
git clone -b manyuser https://github.com/uykb/shadowsocks-rm.git
移动指定文件夹
mv shadowsocks-rm/shadowsocks/ /usr/local/
配置进程守护
echo '[program:shadowsocks]
command=python /usr/local/shadowsocks/servers.py
autorestart=true
user=root' >> /etc/supervisor/conf.d/shadowsocks.conf && echo 'ulimit -n 51200
ulimit -Sn 4096
ulimit -Hn 8192' >> /etc/profile && echo 'ulimit -n 51200
ulimit -Sn 4096
ulimit -Hn 8192' >> /etc/default/supervisor
修改数据库
vim /usr/local/shadowsocks/config.py
启动
service supervisor start 
supervisorctl reload
添加开机自启
vim /etc/rc.local 
service supervisor start
supervisorctl reload
启用算法
apt-get install m2crypto gcc -y
wget -N --no-check-certificate https://download.libsodium.org/libsodium/releases/libsodium-1.0.8.tar.gz
tar zfvx libsodium-1.0.8.tar.gz
cd libsodium-1.0.8
./configure
make && make install
echo "include ld.so.conf.d/*.conf" > /etc/ld.so.conf
echo "/lib" >> /etc/ld.so.conf
echo "/usr/lib64" >> /etc/ld.so.conf
echo "/usr/local/lib" >> /etc/ld.so.conf
ldconfig

Debian / Ubuntu:

    apt-get install python-pip
    pip install shadowsocks

CentOS:

    yum install python-setuptools && easy_install pip
    pip install shadowsocks

Windows:

See [Install Server on Windows]

### Usage

    ssserver -p 443 -k password -m aes-256-cfb

To run in the background:

    sudo ssserver -p 443 -k password -m aes-256-cfb --user nobody -d start

To stop:

    sudo ssserver -d stop

To check the log:

    sudo less /var/log/shadowsocks.log

Check all the options via `-h`. You can also use a [Configuration] file
instead.

Documentation
-------------

You can find all the documentation in the [Wiki].

License
-------

Apache License







[Build Status]:      https://img.shields.io/travis/shadowsocks/shadowsocks/master.svg?style=flat
[Coverage Status]:   https://jenkins.shadowvpn.org/result/shadowsocks
[Coverage]:          https://jenkins.shadowvpn.org/job/Shadowsocks/ws/PYENV/py34/label/linux/htmlcov/index.html
[PyPI]:              https://pypi.python.org/pypi/shadowsocks
[PyPI version]:      https://img.shields.io/pypi/v/shadowsocks.svg?style=flat
[Travis CI]:         https://travis-ci.org/shadowsocks/shadowsocks


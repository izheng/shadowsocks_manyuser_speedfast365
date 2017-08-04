mkdir /project
cd /project

clone https://github.com/ShenYinjie/shadowsocks_manyuser_speedfast365.git

修改 /project/shadowsocks_manyuser_speedfast365/shadowsocks/config.py 中的mysql服务器配置以下几行：
============================
MYSQL_HOST = 'SERVER_IP'
MYSQL_PORT = 3306
MYSQL_USER = '****'
MYSQL_PASS = '****'
MYSQL_DB = '****'

==============

apt-get install python-pip

pip install cymysql

apt-get install supervisor

========

vim /etc/supervisor/conf.d/shadowsocks.conf

在shadowsocks.conf文件里编辑添加：

[program:shadowsocks]
command=python /project/shadowsocks_manyuser_speedfast365/shadowsocks/servers.py
user=root
autostart = true
autoresart = true
stderr_logfile = /var/log/shadowsocks_supervistor.log
stdout_logfile = /var/log/shadowsocks_supervistor.log
stderr_logfile_maxbytes=4MB
stderr_logfile_backups=10
startsecs=3

========


修改以下文件

/etc/profile
/etc/default/supervisor

在文件结尾处添加以下3行内容

ulimit -n 51200
ulimit -Sn 4096
ulimit -Hn 8192

==============

service supervisor start

supervisorctl stop

supervisorctl start

supervisorctl reload



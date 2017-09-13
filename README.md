系统要求：建议 Debian 8 （Aliyun、Vultr、Linode全部没有问题）

<p>
	mkdir /project<br />
cd /project<br />
<br />
clone https://github.com/ShenYinjie/shadowsocks_manyuser_speedfast365.git<br />
<br />
修改 /project/shadowsocks_manyuser_speedfast365/shadowsocks/config.py 中的mysql服务器配置以下几行：<br />
============================<br />
MYSQL_HOST = 'SERVER_IP'<br />
MYSQL_PORT = 3306<br />
MYSQL_USER = '****'<br />
MYSQL_PASS = '****'<br />
MYSQL_DB = '****'<br />
<br />
==============<br />
<br />
apt-get install python-pip<br />
<br />
pip install cymysql<br />
<br />
apt-get install supervisor<br />
<br />
========<br />
<br />
vim /etc/supervisor/conf.d/shadowsocks.conf<br />
<br />
在shadowsocks.conf文件里编辑添加：<br />
<br />
<br />
[program:shadowsocks]<br />
command=python /project/shadowsocks_manyuser_speedfast365/shadowsocks/servers.py<br />
user=root<br />
autostart = true<br />
autoresart = true<br />
stderr_logfile = /var/log/shadowsocks_supervistor.log<br />
stdout_logfile = /var/log/shadowsocks_supervistor.log<br />
stderr_logfile_maxbytes=4MB<br />
stderr_logfile_backups=10<br />
startsecs=3<br />
<br />
========<br />
<br />
<br />
修改以下文件<br />
<br />
/etc/profile<br />
/etc/default/supervisor<br />
<br />
在文件结尾处添加以下3行内容<br />
<br />
ulimit -n 512000<br />
ulimit -Sn 40960<br />
ulimit -Hn 81920<br />
<br />
==============<br />
<br />
service supervisor start<br />
<br />
supervisorctl stop<br />
<br />
supervisorctl start<br />
<br />
supervisorctl reload<br />
<br />
<br />
init 6
</p>
<p>
	<br />
</p>

常用docker 命令

```sh
docker search 镜像名称 //搜索镜像
docker pull 镜像名称:版本号 //拉取对应版本的镜像
docker pull 镜像名称 //默认拉取最新的镜像
docker images //查看本地已下载的镜像
docker ps //查看正在运行的容器
docker ps -a //查看所有的容器（包括run、stop、exited状态的）
docker container ls //查看正在运行的容器
docker rm 容器ID //只能删除没有在运行的容器
docker rm -f 容器ID //可以删除正在运行的容器
docker run -p 本地主机端口号:容器服务端口号 --name 容器名字 [-e 配置信息修改] -d 镜像名字
docker start 容器ID //启动容器
docker stop 容器ID //终止容器
docker rmi 镜像名称orID //删除镜像
重启docker 镜像自动运行
docker run -id --restart=always  镜像名称:tag 容器还没有创建，在运行容器的时候加入–restart=always参数
docker update --restart=always 容器名字或者容器ID   容器已经运行的情况，运行以下命令：
docker update --restart=no 容器名字或者容器ID   停止自动启动
```

postgersql
==========

参考：<https://gitee.com/AiShiYuShiJiePingXing/postgres/blob/master/12.PostgreSQL%20%E5%AE%89%E8%A3%85%E4%B8%8E%E9%83%A8%E7%BD%B2/PostgreSQL%E7%9A%84Docker%E5%AE%89%E8%A3%85%E4%B8%8E%E9%83%A8%E7%BD%B2.md>|

创建数据劵
-----

```sh
docker volume create pgdata
docker volume inspect pgdata
```

安装postgresql
------------

```sh
docker pull postgresql
docker run --name postgres2 -e POSTGRES_PASSWORD=password -p 5432:5432 -v pgdata:/var/lib/docker/volumes/pgdata/_data -d postgres:9.6
docker exec -it postgres2 bash
psql -h localhost -p 5432 -U postgres --password
select * from pg_tables;
```

docker 部署带
----------

扩展的postgresql
-------------

```sh
docker pull kartoza/postgis:9.6-2.4
docker run -d --name postgresql9.6 -e ALLOW_IP_RANGE=0.0.0.0/0 -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=postgres -v pgdata:/var/lib/postgresql/data -p 5432:5432 kartoza/postgis:9.6-2.4


psql -h localhost -p 5432 -U postgres --password
select * from pg_tables;
```

* -e ALLOW\_IP\_RANGE=0.0.0.0/0，这个表示允许所有ip访问，如果不加，则非本机 ip 访问不了
* -e POSTGRES\_USER=postgres 用户名
* -e POSTGRES\_PASS=‘postgres’ 指定密码

m1

```sh
docker pull gangstead/postgis:13-3.1-arm
docker run -d --name postgresql -e ALLOW_IP_RANGE=0.0.0.0/0 -e POSTGRES_USER=postgres -e POSTGRES_PASSWORD=postgres -v pgdata:/var/lib/postgresql/data -p 5432:5432 gangstead/postgis:13-3.1-arm
```

redis
=====

参考：[https://blog.csdn.net/weixin\_38958597/article/details/106048983](https://blog.csdn.net/weixin_38958597/article/details/106048983)

```sh
docker pull redis:latest
docker run -itd -p 6379:6379 --name redis -v /Users/henrydu/Documents/dokcer_config/redis/conf/redis.conf:/etc/redis/redis.conf -v /Users/henrydu/Documents/dokcer_config/redis/data:/data redis redis-server /etc/redis/redis.conf 
```

```sh
// 未配置本地conf时相关参数
-d                                                  -> 以守护进程的方式启动容器
-p 6379:6379                                        -> 绑定宿主机端口
--name myredis                                      -> 指定容器名称
--restart always                                    -> 开机启动
--privileged=true                                   -> 提升容器内权限
-v /root/docker/redis/conf:/etc/redis/redis.conf    -> 映射配置文件
-v /root/docker/redis/data:/data                    -> 映射数据目录
--appendonly yes                                    -> 开启数据持久化
```

mysql
=====

参考：[https://blog.csdn.net/lanpiao\_87/article/details/86064826](https://blog.csdn.net/lanpiao_87/article/details/86064826)

```sh
docker pull mysql:8.0

docker run -di --name=mysql \
-v /Users/henrydu/Documents/dokcer_config/mysql/data:/var/lib/mysql \
-v /Users/henrydu/Documents/dokcer_config/mysql/conf/my.cnf:/etc/mysql/my.cnf \
--privileged=true \
-p 3306:3306 \
-e MYSQL_ROOT_PASSWORD=707116148 {容器ID} \
--lower_case_table_names=1
```

```sh
[client]
default-character-set=utf8mb4
 
[mysql]
default-character-set=utf8mb4
 
[mysqld]
pid-file        = /var/run/mysqld/mysqld.pid
socket          = /var/run/mysqld/mysqld.sock
datadir         = /var/lib/mysql
secure-file-priv= NULL
# Disabling symbolic-links is recommended to prevent assorted security risks
symbolic-links=0
max_connections=10000
default-time_zone='+8:00'
character-set-client-handshake=FALSE
character_set_server=utf8mb4
collation-server=utf8mb4_unicode_ci
init_connect='SET NAMES utf8mb4 COLLATE utf8mb4_unicode_ci'
# Custom config should go here
!includedir /etc/mysql/conf.d/
```

```mysql
-- 远程连接新建用户
mysql> CREATE USER 'henrydu'@'localhost' IDENTIFIED BY '707116148';
Query OK, 0 rows affected (0.05 sec)

mysql> GRANT ALL PRIVILEGES ON *.* TO 'henrydu'@'localhost' WITH GRANT OPTION;
Query OK, 0 rows affected, 1 warning (0.01 sec)

mysql> CREATE USER 'henrydu'@'%' IDENTIFIED BY '707116148';
Query OK, 0 rows affected (0.01 sec)

mysql> GRANT ALL PRIVILEGES ON *.* TO 'henrydu'@'%' WITH GRANT OPTION;
Query OK, 0 rows affected (0.02 sec)

mysql> flush privileges;
Query OK, 0 rows affected (0.00 sec)
```



M1

### mysql8版本

```sh
docker pull mysql/mysql-server
# 其余同上
docker run -di --name=mysql \
-v /Users/henrydu/Documents/dokcer_config/mysql/data:/var/lib/mysql \
-v /Users/henrydu/Documents/dokcer_config/mysql/conf/my.cnf:/etc/mysql/my.cnf \
--privileged=true \
-p 3306:3306 \
-e MYSQL_ROOT_PASSWORD=707116148 {容器ID} \
--lower_case_table_names=1
```

```sh
# 备注：
# 查找Docker内，MySQL配置文件my.cnf的位置
mysql --help | grep my.cnf

# 用户可远程访问
# 查看当前可远程访问账户列表
select host,user,plugin from mysql.user;
# 修改账户信息
update mysql.user set host='%' where user='root';

# 最终结果
mysql> select host,user,plugin from mysql.user;
+-----------+------------------+-----------------------+
| host      | user             | plugin                |
+-----------+------------------+-----------------------+
| %         | root             | caching_sha2_password |
| localhost | healthchecker    | caching_sha2_password |
| localhost | mysql.infoschema | caching_sha2_password |
| localhost | mysql.session    | caching_sha2_password |
| localhost | mysql.sys        | caching_sha2_password |
+-----------+------------------+-----------------------+
5 rows in set (0.00 sec)
```

### mariadb版本（弃用）

```sh
docker pull mariadb
docker run -di --name=mysql \
-v /Users/henrydu/Documents/dokcer_config/mysql/data:/var/lib/mysql \
-v /Users/henrydu/Documents/dokcer_config/mysql/conf/my.cnf:/etc/mysql/my.cnf \
--privileged=true \
-p 3306:3306 \
-e MYSQL_ROOT_PASSWORD=707116148 7eda4c38372f \
--lower_case_table_names=1
```

```sh
# The MariaDB configuration file
#
# The MariaDB/MySQL tools read configuration files in the following order:
# 0. "/etc/mysql/my.cnf" symlinks to this file, reason why all the rest is read.
# 1. "/etc/mysql/mariadb.cnf" (this file) to set global defaults,
# 2. "/etc/mysql/conf.d/*.cnf" to set global options.
# 3. "/etc/mysql/mariadb.conf.d/*.cnf" to set MariaDB-only options.
# 4. "~/.my.cnf" to set user-specific options.
#
# If the same option is defined multiple times, the last one will apply.
#
# One can use all long options that the program supports.
# Run program with --help to get a list of available options and with
# --print-defaults to see which it would actually understand and use.
#
# If you are new to MariaDB, check out https://mariadb.com/kb/en/basic-mariadb-articles/

#
# This group is read both by the client and the server
# use it for options that affect everything
#
[client-server]
# Port or socket location where to connect
port = 3306
socket = /run/mysqld/mysqld.sock

# Import all .cnf files from configuration directory
[mariadbd]
skip-host-cache
skip-name-resolve

!includedir /etc/mysql/mariadb.conf.d/
!includedir /etc/mysql/conf.d/
```



nginx
=====

参考：<https://juejin.cn/post/6977332018140938248>

```sh
docker run --privileged=true \
  --restart=always \
  --name nginx \
  -d -p 80:80 \
  -v /Users/henrydu/Documents/dokcer_config/nginx/data/html:/usr/share/nginx/html \
  -v /Users/henrydu/Documents/dokcer_config/nginx/conf/nginx.conf:/etc/nginx/nginx.conf:ro \
  -v /Users/henrydu/Documents/dokcer_config/nginx/conf/conf.d:/etc/nginx/conf.d \
  -v /Users/henrydu/Documents/dokcer_config/nginx/log:/var/log/nginx \
  nginx
```

配置示例：

location / {

 root /usr/share/nginx/html/templates;

 index index.html index.htm;

 }

 location /images/ {

 root /usr/share/nginx/html/static/;

 }

 location /css/ {

 root /usr/share/nginx/html/static/;

 }

 location /js/ {

 root /usr/share/nginx/html/static/;

 }

location /userimgs/ {

 alias /usr/share/nginx/html/static/images/;

 }

### 原版配置文件：



\# /etc/nginx/nginx.conf

user nginx;

worker\_processes auto;

error\_log /var/log/nginx/error.log notice;

pid /var/run/nginx.pid;

events {

 worker\_connections 1024;

}

http {

 include /etc/nginx/mime.types;

 default\_type application/octet-stream;

 log\_format main '$remote\_addr - $remote\_user [$time\_local] "$request" '

 '$status $body\_bytes\_sent "$http\_referer" '

 '"$http\_user\_agent" "$http\_x\_forwarded\_for"';

 access\_log /var/log/nginx/access.log main;

 sendfile on;

 \#tcp\_nopush on;

 keepalive\_timeout 65;

 \#gzip on;

 include /etc/nginx/conf.d/\*.conf;

}



\# vim /etc/nginx/conf.d/default.conf

server {

 listen 80;

 listen [::]:80;

 server\_name localhost;

 \#access\_log /var/log/nginx/host.access.log main;

 location / {

 root /usr/share/nginx/html;

 index index.html index.htm;

 }

 \#error\_page 404 /404.html;

 \# redirect server error pages to the static page /50x.html

 \#

 error\_page 500 502 503 504 /50x.html;

 location = /50x.html {

 root /usr/share/nginx/html;

 }

 \# proxy the PHP scripts to Apache listening on 127.0.0.1:80

 \#

 \#location ~ \\.php$ {

 \# proxy\_pass http://127.0.0.1;

 \#}

 \# pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000

 \#

 \#location ~ \\.php$ {

 \# root html;

 \# fastcgi\_pass 127.0.0.1:9000;

 \# fastcgi\_index index.php;

 \# fastcgi\_param SCRIPT\_FILENAME /scripts$fastcgi\_script\_name;

 \# include fastcgi\_params;

 \#}

 \# deny access to .htaccess files, if Apache's document root

 \# concurs with nginx's one

 \#

 \#location ~ /\\.ht {

 \# deny all;

 \#}

}

\# vim 50x.html

**\<!DOCTYPE html\>**

**\<****html****\>**

**\<****head****\>**

**\<****title****\>****Error****\</****title****\>**

**\<****style****\>**

**html** **{** **color**-scheme: light dark; **}**

**body** **{** **width**: **35em**; **margin**: **0** **auto**;

**font-family**: **Tahoma****,** **Verdana****,** **Arial****,** **sans-serif**; **}**

**\</****style****\>**

**\</****head****\>**

**\<****body****\>**

**\<****h1****\>****An error occurred.****\</****h1****\>**

**\<****p****\>**Sorry, the page you are looking for is currently unavailable.**\<****br****/\>**

Please try again later.**\</****p****\>**

**\<****p****\>**If you are the system administrator of this resource then you should check

the error log for details.**\</****p****\>**

**\<****p****\>\<****em****\>***Faithfully yours, nginx.***\</****em****\>\</****p****\>**

**\</****body****\>**

**\<****/****html****\>**

\# vim index.html

**\<!DOCTYPE html\>**

**\<****html****\>**

**\<****head****\>**

**\<****title****\>****Welcome to nginx!****\</****title****\>**

**\<****style****\>**

**html** **{** **color**-scheme: light dark; **}**

**body** **{** **width**: **35em**; **margin**: **0** **auto**;

**font-family**: **Tahoma****,** **Verdana****,** **Arial****,** **sans-serif**; **}**

**\</****style****\>**

**\</****head****\>**

**\<****body****\>**

**\<****h1****\>****Welcome to nginx!****\</****h1****\>**

**\<****p****\>**If you see this page, the nginx web server is successfully installed and

working. Further configuration is required.**\</****p****\>**

**\<****p****\>**For online documentation and support please refer to

**\<****a**** ****href****=****"http://nginx.org/"****\>****nginx.org****\</****a****\>**.**\<****br****/\>**

Commercial support is available at

**\<****a**** ****href****=****"http://nginx.com/"****\>****nginx.com****\</****a****\>**.**\</****p****\>**

**\<****p****\>\<****em****\>***Thank you for using nginx.***\</****em****\>\</****p****\>**

**\</****body****\>**

**\<****/****html****\>**

RabbitMQ
========

```python
docker run -it -d --restart=always --name rabbitmq -p 5672:5672 -p 15672:15672 rabbitmq:3.9-management
-- 默认密码guest
```





```sh
docker run -it -d -p 5044:5044 --name logstash --net somenetwork -v /Users/henrydu/Documents/dokcer_config/ELK/logstash/logstash.yml:/usr/share/logstash/config/logstash.yml -v /Users/henrydu/Documents/dokcer_config/ELK/logstash/conf.d/:/usr/share/logstash/conf.d/ logstash:7.1.1
```

```sh
docker run --name filebeat --user=root -d --net somenetwork --volume="/Users/henrydu/Documents/dokcer_config/nginx/log:/var/log/nginx/" --volume="/Users/henrydu/Documents/dokcer_config/ELK/filebeat/filebeat.docker.yml:/usr/share/filebeat/filebeat.yml:ro" --volume="/var/lib/docker/containers:/var/lib/docker/containers:ro" --volume="/var/run/docker.sock:/var/run/docker.sock:ro" store/elastic/filebeat:7.1.1
```














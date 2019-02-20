# ELK配置说明

### 组件:
> 必备组件
java8
nginx
Elasticsearch
Logstash
Kibana

> 其他配置:
redis
Beats
geoip
grafana

### 安装:
#### 下载:
> java8:
`apt search openjdk`
`sudo apt-get install openjdk-8-jdk`

> Elasticsearch:
`wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.6.0.tar.gz`

> Logstash:
`wget https://artifacts.elastic.co/downloads/logstash/logstash-6.6.0.tar.gz`

> Kibana:
`wget https://artifacts.elastic.co/downloads/kibana/kibana-6.6.0-linux-x86_64.tar.gz`

> nginx:
`wget http://nginx.org/download/nginx-1.15.8.tar.gz`
`wget https://ftp.pcre.org/pub/pcre/pcre-8.36.tar.gz`
`wget http://www.zlib.net/zlib-1.2.11.tar.gz`

#### 安装&配置:

##### nginx:
`tar -xzvf nginx-1.15.8.tar.gz`
`tar -xzvf pcre-8.36.tar.gz`
`tar -xzvf zlib-1.2.11.tar.gz`
> 安装pcre
`cd pcre-8.36`
`sudo ./configure `
`sudo make`
`sudo make install`

> 安装zlib
`cd zlib-1.2.11`
`sudo ./configure `
`sudo make`
`sudo make install`

> 安装nginx
> 参考:https://www.cnblogs.com/EasonJim/p/7806879.html
> 参考:https://www.cnblogs.com/keithtt/p/6593866.html
> 参考:https://blog.csdn.net/dawn_02/article/details/82589862
`cd nginx-1.15.8`
pcre 和 zlib的源文件路径要检查对应:
`./configure --prefix=/usr/local/nginx --with-pcre=/home/ubuntu/nginx/pcre-8.36 --with-zlib=/home/ubuntu/nginx/zlib-1.2.11`
`sudo make`
`sudo make install`
```
http {
    include       mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  logs/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    #keepalive_timeout  0;
    keepalive_timeout  65;

    #gzip  on;

server {
        listen 80;
        server_name 172.21.0.9;    #当前主机名
        #auth_basic "Restricted Access";
        #auth_basic_user_file /usr/local/nginx/conf/htpasswd.users;      #登录验证
        location / {
        proxy_pass http://172.21.0.9:5601;     #转发到kibana
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
                }
        }
```




##### Elasticsearch:
`tar -xzvf elasticsearch-6.6.0.tar.gz`
`cd elasticsearch-6.6.0`
`sudo vim elasticsearch-6.6.0/config/elasticsearch.yml`
```yml
cluster.name: elk
node.name: node-1
path.data: /home/ubuntu/elasticsearch-6.6.0/data
path.logs: /home/ubuntu/elasticsearch-6.6.0/logs
# bootstrap.memory_lock: flase
# bootstrap.system_call_filter:false
network.host: 172.21.0.9
http.port: 9200
```
`sudo vim jvm.options`
```
Xms512m
-Xmx512m
```


##### Logstash:
`tar -xzvf logstash-6.6.0.tar.gz`
`cd logstash-6.6.0`
`sudo vim elk_nginx_log`
`sudo vim jvm.options`
```
Xms512m
-Xmx512m
```

##### Kibana:
`tar -xzvf kibana-6.6.0-linux-x86_64.tar.gz`
`cd kibana-6.6.0-linux-x86_64`
`sudo vim /kibana-6.6.0-linux-x86_64/config/kibana.yml`
```yml
server.host: "172.21.0.9"
elasticsearch.hosts: "http://172.21.0.9:9200"
elasticsearch.requestTimeout: 100000
```


#### 启动
> nginx:
sudo /usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf
注意：-c 指定配置文件的路径，不加的话，nginx会自动加载默认路径的配置文件，可以通过-h查看帮助命令。
重启:/usr/local/nginx/sbin/nginx -s reload
#查看进程：
ps -ef | grep nginx

> Elasticsearch:
`bin/elasticsearch`


> Logstash:
`bin/logstash -f elk_nginx_log.conf `
> 参考https://www.elastic.co/guide/en/logstash/current/config-examples.html

> Kibana:
`bin/kibana -d`



### 其他组件
#####  redis
> 参考:http://blog.51cto.com/jinlong/2056563
#####  Beats
#####  geoip
> 参考:http://blog.51cto.com/nosmoking/1873879
##### grafana
> 参考:https://grafana.com/dashboards/2292


## 其他相关
> 参考:https://blog.csdn.net/weixin_39800144/article/details/81162002
```
[1]不能用root用户启动Elasticsearch
[2]Elasticsearch用户拥有的内存权限太小，至少需要262144；
解决：
切换到root用户
执行命令：
sysctl -w vm.max_map_count=262144
查看结果：
sysctl -a|grep vm.max_map_count
显示：
vm.max_map_count = 262144
上述方法修改之后，如果重启虚拟机将失效，所以：
解决办法：
在  /etc/sysctl.conf文件最后添加一行
vm.max_map_count=262144
```

> nginx 安装路径
```
  nginx path prefix: "/usr/local/nginx"
  nginx binary file: "/usr/local/nginx/sbin/nginx"
  nginx modules path: "/usr/local/nginx/modules"
  nginx configuration prefix: "/usr/local/nginx/conf"
  nginx configuration file: "/usr/local/nginx/conf/nginx.conf"
  nginx pid file: "/usr/local/nginx/logs/nginx.pid"
  nginx error log file: "/usr/local/nginx/logs/error.log"
  nginx http access log file: "/usr/local/nginx/logs/access.log"
  nginx http client request body temporary files: "client_body_temp"
  nginx http proxy temporary files: "proxy_temp"
  nginx http fastcgi temporary files: "fastcgi_temp"
  nginx http uwsgi temporary files: "uwsgi_temp"
  nginx http scgi temporary files: "scgi_temp"
```

> 全成卸载nginx
```
sudo apt-get remove nginx nginx-common # 卸载删除除了配置文件以外的所有文件。
sudo apt-get purge nginx nginx-common # 卸载所有东东，包括删除配置文件。
sudo apt-get autoremove # 在上面命令结束后执行，主要是卸载删除Nginx的不再被使用的依赖包。
sudo apt-get remove nginx-full nginx-common #卸载删除两个主要的包。
sudo service nginx restart  #重启nginx检测是否存在
```









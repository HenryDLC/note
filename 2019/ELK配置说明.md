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


#### 解压:
`tar -xzvf elasticsearch-6.6.0.tar.gz`
`tar -xzvf kibana-6.6.0-linux-x86_64.tar.gz`
`tar -xzvf logstash-6.6.0.tar.gz`


#### 安装&配置:

##### nginx:
###### 安装依赖
`tar -xzvf nginx-1.15.8.tar.gz`
`tar -xzvf pcre-8.36.tar.gz`
`tar -xzvf zlib-1.2.11.tar.gz`
> 安装pcre
cd pcre-8.36
./configure 
make && make install

> 安装zlib
cd zlib-1.2.11
./configure 
make && make install

> 安装nginx
cd nginx-1.15.8
./configure ./configure --prefix=/usr/local/nginx --with-pcre=/home/ubuntu/nginx/pcre-8.36 --with-zlib=/home/ubuntu/nginx/zlib-1.2.11
make && make install



##### Elasticsearch:
`cd elasticsearch`
`sudo vim elasticsearch-6.6.0/config/elasticsearch.yml`
```yml
cluster.name: elk
node.name: node-1
path.data: /home/ubuntu/ekl/elasticsearch-6.6.0/data
path.logs: /home/ubuntu/ekl/elasticsearch-6.6.0/logs
bootstrap.memory_lock: flase
bootstrap.system_call_filter:false
network.host: 172.21.0.9
http.port: 9200

```


##### Logstash:


##### Kibana:
`cd elasticsearch`
`sudo vim /kibana-6.6.0-linux-x86_64/config/kibana.yml`
>cluster.name: elk
```yml
server.host: "172.21.0.9"
elasticsearch.hosts: ["http://172.21.0.9:9200"]
```



#### 启动
> nginx:
sudo /usr/local/nginx/sbin/nginx -c /usr/local/nginx/conf/nginx.conf
注意：-c 指定配置文件的路径，不加的话，nginx会自动加载默认路径的配置文件，可以通过-h查看帮助命令。
#查看进程：
ps -ef | grep nginx

> Elasticsearch:
`bin/elasticsearch -d
`
> Logstash:
> 参考https://www.elastic.co/guide/en/logstash/current/config-examples.html

> Kibana:
`bin/kibana -d`






### 其他组件
#####  redis
#####  Beats
#####  geoip

## 其他相关
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
/usr/sbin/nginx：主程序
/etc/nginx：存放配置文件
/usr/share/nginx：存放静态文件
/var/log/nginx：存放日志
```

> 完成卸载nginx
```
sudo apt-get remove nginx nginx-common # 卸载删除除了配置文件以外的所有文件。
sudo apt-get purge nginx nginx-common # 卸载所有东东，包括删除配置文件。
sudo apt-get autoremove # 在上面命令结束后执行，主要是卸载删除Nginx的不再被使用的依赖包。
sudo apt-get remove nginx-full nginx-common #卸载删除两个主要的包。
sudo service nginx restart  #重启nginx检测是否存在
```
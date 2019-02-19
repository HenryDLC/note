# ELK配置说明

### 组件:
> 必备组件
java8
nginx
Elasticsearch
Kibana
Logstash

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

> Kibana:
`wget https://artifacts.elastic.co/downloads/kibana/kibana-6.6.0-linux-x86_64.tar.gz`

> Logstash:
`wget https://artifacts.elastic.co/downloads/logstash/logstash-6.6.0.tar.gz`

> nginx:
`sudo apt-get install nginx`

#### 解压:
`tar -xzvf elasticsearch-6.6.0.tar.gz`
`tar -xzvf kibana-6.6.0-linux-x86_64.tar.gz`
`tar -xzvf logstash-6.6.0.tar.gz`

#### 配置:
##### Elasticsearch:
`cd elasticsearch`
`sudo vim elasticsearch-6.6.0/config/elasticsearch.yml`
>cluster.name: elk
```yml
node.name: node-1
path.data: /home/ubuntu/ekl/elasticsearch-6.6.0/data
path.logs: /home/ubuntu/ekl/elasticsearch-6.6.0/logs
bootstrap.memory_lock: flase
bootstrap.system_call_filter:false
network.host: 172.21.0.9
http.port: 9200

```



##### Kibana:

##### Logstash:

##### nginx:


#### 启动
> Elasticsearch:
`bin/elasticsearch -d
`

> Kibana:


> Logstash:


> nginx:
`service nginx start|stop|reload`

### 其他组件







##其他相关
```
注意:
不能用root用户启动Elasticsearch
```

```
elasticsearch启动时遇到的错误
问题翻译过来就是：elasticsearch用户拥有的内存权限太小，至少需要262144；
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


> 卸载nginx
```
sudo apt-get remove nginx nginx-common # 卸载删除除了配置文件以外的所有文件。
sudo apt-get purge nginx nginx-common # 卸载所有东东，包括删除配置文件。
sudo apt-get autoremove # 在上面命令结束后执行，主要是卸载删除Nginx的不再被使用的依赖包。
sudo apt-get remove nginx-full nginx-common #卸载删除两个主要的包。
sudo service nginx restart  #重启nginx
```
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
`https://artifacts.elastic.co/downloads/kibana/kibana-6.6.0-linux-x86_64.tar.gz`

> Logstash:
`https://artifacts.elastic.co/downloads/logstash/logstash-6.6.0.tar.gz`

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
network.host: 172.21.0.9
http.port: 9200
```
```

> Kibana:
`https://artifacts.elastic.co/downloads/kibana/kibana-6.6.0-linux-x86_64.tar.gz`

> Logstash:
`https://artifacts.elastic.co/downloads/logstash/logstash-6.6.0.tar.gz`

> nginx:
`sudo apt-get install nginx`



### 其他组件
# 创建Googlecloud实例
![WechatIMG3.png](1)
# 创建防火墙出入站规则
## 入站
![WechatIMG4.png](2)
## 出站
![WechatIMG5.png](3)
# 登入SSH配置服务器
## 获取root
`sudo -i`
## 开启bbr
`wget --no-check-certificate -O tcp.sh https://github.com/cx9208/Linux-NetSpeed/raw/master/tcp.sh && chmod +x tcp.sh && ./tcp.sh`
## 时间校准
### 查看当前时间
`date -R`
### 修改服务器时间(当服务器与本地时间不一致时)
`sudo date --set="2017-01-22 16:16:23"`
# 
$ wget https://install.direct/go.sh
--2018-03-17 22:49:09--  https://install.direct/go.sh
Resolving install.direct (install.direct)... 104.27.174.71, 104.27.175.71, 2400:cb00:2048:1::681b:af47, ...
Connecting to install.direct (install.direct)|104.27.174.71|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: unspecified [text/plain]
Saving to: ‘go.sh’

go.sh                             [ <=>                                                 ]  11.24K  --.-KB/s    in 0.001s  

2018-03-17 22:49:09 (17.2 MB/s) - ‘go.sh’ saved [11510]


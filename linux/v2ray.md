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
# 安装V2ray
`wget https://install.direct/go.sh`
## 执行脚本
`sudo bash go.sh`
## 开启v2ray服务
`sudo systemctl start v2ray`


# 谷歌服务起搭建v2ray服务
## 创建Googlecloud实例
![image](https://github.com/HenryDLC/note/blob/master/linux/image/WechatIMG3.png)
## 创建防火墙出入站规则
### 入站
![image](https://github.com/HenryDLC/note/blob/master/linux/image/WechatIMG4.png)
### 出站
![image](https://github.com/HenryDLC/note/blob/master/linux/image/WechatIMG5.png)
## 登入SSH配置服务器
### 获取root
`sudo -i`
### 开启bbr
`wget --no-check-certificate -O tcp.sh https://github.com/cx9208/Linux-NetSpeed/raw/master/tcp.sh && chmod +x tcp.sh && ./tcp.sh`
### 时间校准
#### 查看当前时间
`date -R`
#### 修改服务器时间(当服务器与本地时间不一致时)
`sudo date --set="2020-03-22 15:14:00"`
## 安装V2ray
`wget https://install.direct/go.sh`
### 执行脚本
`sudo bash go.sh`
### 开启v2ray服务
`sudo systemctl start v2ray`> 段落引用
### 查看v2ray账号
`cat /etc/v2ray/config.json `> 段落引用

## 配置客户端
#### 配置要求:
```json
{
  "inbounds": [
    {
      "port": 1080, // 监听端口
      "protocol": "socks", // 入口协议为 SOCKS 5
      "sniffing": {
        "enabled": true,
        "destOverride": ["http", "tls"]
      },
      "settings": {
        "auth": "noauth"  //socks的认证设置，noauth 代表不认证，由于 socks 通常在客户端使用，所以这里不认证
      }
    }
  ],
  "outbounds": [
    {
      "protocol": "vmess", // 出口协议
      "settings": {
        "vnext": [
          {
            "address": "serveraddr.com", // 服务器地址，请修改为你自己的服务器 IP 或域名
            "port": 16823,  // 服务器端口
            "users": [
              {
                "id": "b831381d-6324-4d53-ad4f-8cda48b30811",  // 用户 ID，必须与服务器端配置相同
                "alterId": 64 // 此处的值也应当与服务器相同
              }
            ]
          }
        ]
      }
    }
  ]
}
```
#### 示例:
```json
{
  "inbounds": [
    {
      "port": 1080, 
      "protocol": "socks", 
      "sniffing": {
        "enabled": true,
        "destOverride": ["http", "tls"]
      },
      "settings": {
        "auth": "noauth"
      }
    }
  ],
  "outbounds": [
    {
      "protocol": "vmess", 
      "settings": {
        "vnext": [
          {
            "address": "34.87.124.228", 
            "port": 19254, 
            "users": [
              {
                "id": "d41970d4-e56f-4a1c-922e-e5cbed28969f", 
                "alterId": 64
              }
            ]
          }
        ]
      }
    }
  ]
}
```
#### 示例:
```json
{
  "inbounds": [
    {
      "port": 1080, 
      "protocol": "socks", 
      "sniffing": {
        "enabled": true,
        "destOverride": ["http", "tls"]
      },
      "settings": {
        "auth": "noauth"
      }
    }
  ],
  "outbounds": [
    {
      "protocol": "vmess", 
      "settings": {
        "vnext": [
          {
            "address": "34.87.168.235", 
            "port": 25868, 
            "users": [
              {
                "id": "404b81ac-72ac-49f0-a1be-92f04014b024", 
                "alterId": 64
              }
            ]
          }
        ]
      }
    }
  ]
}
```


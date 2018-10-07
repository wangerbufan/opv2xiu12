# V2Ray Openshift

## 概述

用于在 Openshift 上部署 V2Ray Websocket。

**Openshift 为我们提供了免费的容器服务，我们不应该滥用它。正因如此，本项目不宜做为长期翻墙使用。**

**Openshift 的网络并不稳定，部署前请三思。**

## 镜像

 - DockerHub 的镜像：`bclswl0827/v2ray-openshift`
 
 ## ENV 设定
 
 ### 单纯地使用 Websocket
 
`CONFIG_JSON` > `服务端配置文件`
 
 ### Websocket + TLS
 
`CONFIG_JSON` > `服务端配置文件`

`CERT_PEM` > `证书文件内容`

`KEY_PEM`  > `私钥文件内容`

---

**事实上，Openshift 配置 Websocket + TLS 用不着第二种方法这么麻烦，只需要配置好 `CONFIG_JSON`，然后在 `Route` 中勾选 `Secure Route` 即可实现 TLS。第二种方法是面向其它容器平台的。**

亦可使用该方法部署到日本的 Arukas 上。请自行变通。

## 注意

设定 ENV 时，务必将配置文件的换行符 `\r\n` 变更为 `\n`，然后填入 ENV 。使用 Linux 的朋友可以不用管这一步。


# v2ray 部署在 openshift 、Arukas等
openshift: 内存设置为256M，每 project 可配置 4 Pods。

Docker 镜像：crownzhu/v2ray:latest

环境变量： CONFIG_JSON（配置）、CERT_PEM（证书）、KEY_PEM（私钥）

用notepad++将上述变量中 \r\n 替换为\\n，变成一行，导入容器。

客户端： android Actinium、windows v2ray 可用同一个服务端。



{
  "log": {
    "loglevel": "warning"
  },
  "inbound": {
    "protocol": "vmess",
    "port": 8080,
    "settings": {
      "clients": [
        {
          "id": "6936eeda-f303-4cc6-965b-fea4433938af",
          "alterId": 64,
          "security": "chacha20-ploy1305"
        }
      ]
    },
    "streamSettings": {
      "network": "ws"
    }
  },
  "inboundDetour": [],
  "outbound": {
    "protocol": "freedom",
   "settings": {}
  }
}


# 使用Heroku部署高性能代理服务Xray vless
## 概述

用于在 Heroku 上部署 vless+websocket+tls，每次部署自动选择最新的 alpine linux 和 Xray core 。  
vless 性能更加优秀，占用资源更少。

**Heroku 为我们提供了免费的容器服务，我们不应该滥用它，所以本项目不宜做为长期翻墙使用。**

在这里感谢bclswl0827提供的v2ray教程。

## 镜像

本镜像不会因为大量占用资源而被封号。注册好Heroku账号并登录后,点击下面按钮便可部署.

[![Deploy](https://www.herokucdn.com/deploy/button.png)](https://dashboard.heroku.com/new?template=https%3A%2F%2Fgithub.com%2Fleyounet%2FXray-Heroku)

### 路径

`WebSocket` 路径(配置文件中的 `path` )为 `/` 。

### 端口

`端口` 为 `443` 。

### UUID

`UUID` 默认为 `24b4b1e1-7a89-45f6-858c-242cf53b5bdb` 可自行设置。

XRay 将在部署时不会自动安装最新版本，目前是1.2.1版。

**出于安全考量，除非使用 CDN，否则请不要使用自定义域名，而使用 Heroku 分配的二级域名，以实现 XRay Websocket + TLS。**

## 流量中转

可以使用cloudflare的workers来`中转流量`，配置为：  

addEventListener(  
    "fetch",event => {  
        let url=new URL(event.request.url);  
        url.hostname="xxx.herokuapp.com";//你的heroku域名    
        let request=new Request(url,event.request);  
        event. respondWith(  
            fetch(request)  
        )  
    }  
)  


## 关于CF筛选IP

请参考 https://github.com/badafans/better-cloudflare-ip/tree/20201208

### 特别感谢 ：

* [bclswl0827](https://github.com/bclswl0827/v2ray-heroku)
* [yxhit](https://github.com/yxhit)
* [badafans](https://github.com/badafans/better-cloudflare-ip/tree/20201208)



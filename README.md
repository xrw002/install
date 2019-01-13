启动容器
docker run -d --name v2ray -v /etc/v2ray:/etc/v2ray --restart=always -p 10086:10086 v2ray/official  v2ray -config=/etc/v2ray/config.json
客户端配置
在这里找一下适合你的系统的客户端程序下载， https://github.com/v2ray/v2ray-core/releases 

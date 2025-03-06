# 原仓库 [SuperNG6](https://github.com/SuperNG6/Docker-qBittorrent-Enhanced-Edition)
### 上游仓库已经不再支持ARMv7，已经添加ARMv7镜像
### 自用镜像，如有问题前请往原仓库

### docker命令行设置：


1. 创建qbittorrent容器

````
docker create  \
    --name=qbittorrentee  \
    -e WEBUIPORT=8080  \
    -e PUID=1000 \
    -e PGID=100 \
    -e TZ=Asia/Shanghai \
    -e WEB_USER=admin \
    -e WEB_PASSWORD=veryscrect \
    -p 6881:6881  \
    -p 6881:6881/udp  \
    -p 8080:8080  \
    -v /配置文件位置:/config  \
    -v /下载位置:/downloads  \
    --restart unless-stopped  \
    weycovo/qbittorrentee:latest
````

### docker-compose
````
version: "2"
services:
  qbittorrentee:
    image: weycovo/qbittorrentee
    container_name: qbittorrentee
    environment:
      - PUID=1000
      - PGID=100
      - TZ=Asia/Shanghai
      - WEB_USER=admin
      - WEB_PASSWORD=veryscrect
    volumes:
      - /path/to/appdata/config:/config
      - /path/to/downloads:/downloads
    ports:
      - 6881:6881
      - 6881:6881/udp
      - 8080:8080
    restart: unless-stopped
````



### 变量:

|参数|说明|
|-|:-|
| `--name=qbittorrentee` |容器名|
| `-p 8080:8080` |web访问端口 [IP:8080](IP:8080);(默认用户名:admin;默认密码为随机生成);此端口需与容器端口和环境变量保持一致，否则无法访问|
| `-p 6881:6881` |BT下载监听端口|
| `-p 6881:6881/udp` |BT下载DHT监听端口
| `-v /配置文件位置:/config` |qBittorrent配置文件位置|
| `-v /下载位置:/downloads` |qBittorrent下载位置|
| `-e WEBUIPORT=8080` |web访问端口环境变量|
| `-e TZ=Asia/Shanghai` |系统时区设置,默认为Asia/Shanghai|
| `-e WEB_USER=admin` |用户名设置,默认为admin|
| `-e WEB_PASSWORD=veryscrect` |明文密码设置,默认为空白|
| `-e WEB_PASSWORD_FILE=/path/to/secrets` |明文密码文件路径,默认为空白|
| `-e WEB_PBKDF2_PASSWORD=@Bytes(...)` |密文密码设置,默认为空白|
| `-e WEB_PBKDF2_PASSWORD_FILE=/path/to/secrets` |密文密码文件路径,默认为空白|

### 群晖docker设置：

1. 卷

|参数|说明|
|-|:-|
| `本地文件夹1:/downloads` |qBittorrent下载位置|
| `本地文件夹2:/config` |qBittorrent配置文件位置|

2. 端口

|参数|说明|
|-|:-|
| `本地端口1:6881` |BT下载监听端口|
| `本地端口2:6881/udp` |BT下载DHT监听端口|
| `本地端口3:8080` |web访问端口 [IP:8080](IP:8080);(默认用户名:admin;默认密码:adminadmin);此端口需与容器端口和环境变量保持一致，否则无法访问|

3. 环境变量：

|参数|说明|
|-|:-|
| `TZ=Asia/Shanghai` |系统时区设置,默认为Asia/Shanghai|
| `WEBUIPORT=8080` |web访问端口环境变量|
| `WEB_USER=admin` |web用户名环境变量|
| `WEB_PASSWORD=veryscrect` |web密码环境变量|
| `WEB_PASSWORD_FILE=/path/to/secrets` |web密码文件环境变量|
| `WEB_PBKDF2_PASSWORD=@Bytes(...)` |web密码密文环境变量|
| `WEB_PBKDF2_PASSWORD_FILE=/path/to/secrets` |web密码密文文件环境变量|

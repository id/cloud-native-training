# 基于 Alpine 镜像
FROM alpine:latest

# 更新包索引并安装 Python
RUN apk update && apk add python3

# 在容器中创建一个目录来存储我们的 index.html 文件
WORKDIR /web

# 将本地的 index.html 文件拷贝到容器的 /web 目录下
COPY .. /web

# 当容器启动运行 Python 的 HTTP 服务器
ENTRYPOINT [ "python3", "-m", "http.server" ]

# 默认启动的 HTTP 服务器监听在 8080 端口
CMD [ "8080" ]

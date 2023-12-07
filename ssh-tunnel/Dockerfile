# 使用具有SSH客户端的轻量级Alpine Linux镜像
FROM alpine:latest

# 安装 openssh-client
RUN apk add --no-cache openssh-client

RUN mkdir /root/.ssh

# 连接时不进行主机密钥验证
RUN echo "Host *" >> /root/.ssh/config
RUN echo "    StrictHostKeyChecking no" >> /root/.ssh/config

# 设置默认环境变量
ENV LOCAL_PORT=50000
ENV REMOTE_PORT=27017
ENV USERNAME=username
ENV REMOTE_IP=remote_IP
ENV REMOTE_HOST=localhost

# 设置启动命令为创建SSH隧道的命令
CMD ssh -N -L *:$LOCAL_PORT:$REMOTE_HOST:$REMOTE_PORT $USERNAME@$REMOTE_IP

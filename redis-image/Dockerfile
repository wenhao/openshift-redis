FROM alpine:latest

RUN set -x \
	&& sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories \
	&& apk add --no-cache redis sed bash tzdata \
	&& cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone \
    && apk del --no-cache tzdata

COPY redis-master.conf /redis/redis-master/redis.conf
COPY redis-slave.conf /redis/redis-slave/redis.conf
COPY run.sh /redis/run.sh

CMD [ "/redis/run.sh" ]

ENTRYPOINT [ "bash", "-c" ]

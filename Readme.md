Redis Alpine

Docker:
```
https://cloud.docker.com/u/afnia/repository/docker/afnia/redis-alpine
```

```
FROM alpine:latest

#RUN addgroup -S redis && adduser -S -G redis redis\
#    && mkdir -p /redis/data /redis/modules\
#    && chown redis:redis /redis/data /redis/modules
RUN set -x\
    && apk add --no-cache --virtual .build-deps\
    curl\
    gcc\
    linux-headers\
    make\
    musl-dev\
    tar\
    && curl -o redis.tar.gz https://codeload.github.com/antirez/redis/tar.gz/5.0.4\
    && mkdir -p /usr/src/redis\
    && tar -xzf redis.tar.gz -C /usr/src/redis --strip-components=1\
    && rm redis.tar.gz\
    && make -C /usr/src/redis\
    && make -C /usr/src/redis install\
    && rm -r /usr/src/redis\
    && apk del .build-deps

VOLUME /redis/modules
VOLUME /redis/data

WORKDIR /redis/data
```

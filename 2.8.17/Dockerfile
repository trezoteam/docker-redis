FROM debian:stretch-slim
RUN apt-get update && apt-get install wget make gcc -y
RUN cd /opt \
    && mkdir redis-server \
    && cd redis-server \
    && wget http://download.redis.io/releases/redis-2.8.17.tar.gz \
    && tar -xf redis-2.8.17.tar.gz \
    && cd redis-2.8.17 \
    && cd deps \
    && make hiredis jemalloc linenoise lua \
    && cd .. \
    && make install \
    && rm -Rf /opt/*

RUN mkdir -p /var/lib/redis
COPY redis.conf /redis.conf

RUN apt-get purge -y wget make gcc --autoremove \
     && rm -Rf /var/cache/*

CMD ["/usr/local/bin/redis-server", "/redis.conf"]

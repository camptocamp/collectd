FROM debian:stable

ENV DEBIAN_FRONTEND noninteractive
COPY 50docker-apt-conf /etc/apt/apt.conf.d/

COPY rootfs_prefix/ /usr/src/

RUN apt-get update \
 && apt-get upgrade \
 && apt-get install \
    collectd-core \
    collectd-utils \
    build-essential \
 && make -C /usr/src/rootfs_prefix/ \
 && apt-get --purge remove build-essential \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

COPY docker-collectd.conf /etc/collectd/

ENV LD_PRELOAD /usr/src/rootfs_prefix/rootfs_prefix.so

CMD [ "/usr/sbin/collectd", "-f", "-C", "/etc/collectd/docker-collectd.conf" ]

ARG BUILD_FROM
FROM $BUILD_FROM

MAINTAINER Matt Longman <git@mattlongman.com>

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

ENV LANG C.UTF-8

RUN apk update && \
apk add --no-cache bash jq iw hostapd networkmanager networkmanager-cli net-tools sudo dnsmasq build-base && \
rm -rf /var/cache/apk/*

COPY hostapd.conf /
COPY dnsmasq.conf /

COPY run.sh /
RUN chmod a+x /run.sh

ADD https://raw.githubusercontent.com/geekman/mdns-repeater/master/mdns-repeater.c mdns-repeater.c
RUN gcc -O3 -o /bin/mdns-repeater mdns-repeater.c -DHGVERSION="\"1\""

CMD [ "/run.sh" ]

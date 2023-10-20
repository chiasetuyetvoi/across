# Dockerfile for xray based alpine
# Copyright (C) 2019 - 2021 Teddysun <i@teddysun.com>
# Reference URL:
# https://github.com/XTLS/Xray-core
# https://github.com/v2fly/v2ray-core
# https://github.com/v2fly/geoip
# https://github.com/v2fly/domain-list-community

# Current version: 3.18.4
FROM alpine:latest
# LABEL maintainer="Teddysun <i@teddysun.com>"
LABEL maintainer="wondershare"

# Expose ports
EXPOSE 9000 80 443

WORKDIR /root
COPY xray.sh /root/xray.sh
COPY config.json /etc/xray/config.json
RUN set -ex \
	&& apk add --no-cache tzdata ca-certificates \
	&& mkdir -p /var/log/xray /usr/share/xray \
	&& chmod +x /root/xray.sh \
	&& /root/xray.sh \
	&& rm -fv /root/xray.sh \
	# && wget -O /usr/share/xray/geosite.dat https://github.com/v2fly/domain-list-community/releases/latest/download/dlc.dat \
	# && wget -O /usr/share/xray/geoip.dat https://github.com/v2fly/geoip/releases/latest/download/geoip.dat
	&& wget -O /usr/share/xray/geosite.dat https://raw.githubusercontent.com/chiasetuyetvoi/across/master/docker/xray/prebuild/dlc.dat \
	&& wget -O /usr/share/xray/geoip.dat https://raw.githubusercontent.com/chiasetuyetvoi/across/master/docker/xray/prebuild/geoip.dat

VOLUME /etc/xray
# ENV TZ=Asia/Shanghai
ENV TZ=Asia/Ho_Chi_Minh
CMD [ "/usr/bin/xray", "-config", "/etc/xray/config.json" ]

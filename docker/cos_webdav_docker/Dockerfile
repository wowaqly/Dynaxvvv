FROM ubuntu:22.04
MAINTAINER wowaqly
ENV WEBDAV_REV "4.2.0"
ENV APT_SOURCE_HOST "mirrors.huaweicloud.com"
ARG DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Shanghai
VOLUME ["/root/data"]
ENV BUCKETNAME_APPID=123
ENV SECRETID=123
ENV SECRETKEY=123
ENV REGION=ap-nanjing
ENV DAV_USER=admin
ENV DAV_PWD=admin

COPY start.sh /root/start.sh
COPY sync.sh /root/sync.sh
COPY zipbak.sh /root/zipbak.sh
RUN sed -i "s@http://.*archive.ubuntu.com@http://${APT_SOURCE_HOST}@g" /etc/apt/sources.list && sed -i "s@http://.*security.ubuntu.com@http://${APT_SOURCE_HOST}@g" /etc/apt/sources.list && apt-get update  && apt-get upgrade -y && apt-get install wget pip cron zip -y
RUN pip install coscmd -i https://repo.huaweicloud.com/repository/pypi/simple --trusted-host repo.huaweicloud.com
RUN mkdir /root/webdavserver && cd /root/webdavserver  && wget https://github.com/hacdias/webdav/releases/download/v${WEBDAV_REV}/linux-amd64-webdav.tar.gz && tar -zxvf linux-amd64-webdav.tar.gz && rm -f /root/webdavserver/linux-amd64-webdav.tar.gz
RUN chmod +x /root/*.sh && mkdir -p /root/data && echo 'PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin' >> /etc/crontab && echo '*/10 * * * * root bash /root/sync.sh'  >> /etc/crontab && echo '0 12 * * * root bash /root/zipbak.sh'  >> /etc/crontab

CMD bash /root/start.sh

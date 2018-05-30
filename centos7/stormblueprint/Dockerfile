FROM base1/centos7
MAINTAINER Wu

# ENV varables.
ENV http_proxy=http://web-proxy.sgp.hpecorp.net:8080
ENV https_proxy=http://web-proxy.sgp.hpecorp.net:8080
ENV WORKDIR=/tmp/ebc
WORKDIR $WORKDIR

# get the tarball.

RUN wget http://www-us.apache.org/dist/zookeeper/zookeeper-3.4.12/zookeeper-3.4.12.tar.gz -P $WORKDIR
RUN wget http://www-us.apache.org/dist/kafka/1.1.0/kafka_2.11-1.1.0.tgz -P $WORKDIR
# unzip the tarball
RUN tar -xvf $WORKDIR/zookeeper-3.4.12.tar.gz -C $WORKDIR
RUN tar -xvf $WORKDIR/kafka_2.11-1.1.0.tgz -C $WORKDIR

# install ebc
# execuable
# update file .bashrc for ebc environment var for bash
# 

EXPOSE 1-65535
FROM centos7/hadoop1a
MAINTAINER Wu

# ENV varables.
# ENV http_proxy=http://web-proxy.sgp.hpecorp.net:8080
# ENV https_proxy=http://web-proxy.sgp.hpecorp.net:8080
ENV WORKDIR=/tmp/wk

WORKDIR $WORKDIR
ENV HADOOP_VERSION=2.9.1
#################################
# Unzip package and remove the original package.
#################################
RUN tar -xvf $WORKDIR/hadoop-${HADOOP_VERSION}.tar.gz -C /opt &&\
	ln -s /opt/hadoop-${HADOOP_VERSION} /opt/hadoop &&\
	rm hadoop-${HADOOP_VERSION}.tar.gz

# docker build --force-rm=true -t centos7/hadoop2a ./

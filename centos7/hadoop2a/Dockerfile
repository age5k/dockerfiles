FROM centos7/hadoop1a
MAINTAINER Wu

# ENV varables.
# ENV http_proxy=http://web-proxy.sgp.hpecorp.net:8080
# ENV https_proxy=http://web-proxy.sgp.hpecorp.net:8080
ENV WORKDIR=/tmp/wk

WORKDIR $WORKDIR
ENV USER_NAME=hadoop
ENV HADOOP_VERSION=2.9.1
#################################
# Unzip package and remove the original package.
#################################
RUN useradd $USER_NAME
RUN tar -xvf $WORKDIR/hadoop-${HADOOP_VERSION}.tar.gz -C /opt &&\	
	ln -s /opt/hadoop-${HADOOP_VERSION} /opt/hadoop &&\	
	chown -R $USER_NAME /opt/hadoop-${HADOOP_VERSION} &&\
	chgrp -R $USER_NAME /opt/hadoop-${HADOOP_VERSION} &&\
	echo 'export HADOOP_HOME=/opt/hadoop' | tee -a /home/$USER_NAME/.bashrc &&\
	echo 'export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin' | tee -a /home/$USER_NAME/.bashrc &&\
	rm hadoop-${HADOOP_VERSION}.tar.gz

# docker build --force-rm=true -t centos7/hadoop2a ./

FROM centos7/mycat1a
MAINTAINER Wu

# ENV varables.

ENV WORKDIR=/tmp/wk
ENV USER_NAME=mycat
WORKDIR $WORKDIR
#################################
# Configurations Step 1
#################################
######{LANG is missing?
RUN echo 'LANG=en_US.UTF-8' >> /etc/bashrc
######}

######{ START CONFIG ENV vars

# 	Configure JAVA_HOME ENV
RUN echo 'export JAVA_HOME=/usr/lib/jvm/java' | tee -a /etc/profile.d/java.sh &&\
	echo 'export PATH=$PATH:$JAVA_HOME/bin' | tee -a /etc/profile.d/java.sh

######} END CONFIG ENV vars
RUN useradd $USER_NAME &&\
	tar -xvf $WORKDIR/Mycat-server-1.6.5-release-20180122220033-linux.tar.gz -C /opt &&\
	ln -s /opt/Mycat-server-1.6.5-release-20180122220033-linux /opt/mycat &&\
	chown -R $USER_NAME:$USER_NAME /opt/Mycat-server-1.6.5-release-20180122220033-linux


EXPOSE 1-65535
# docker build --force-rm=true -t centos7/mycat1c ./
# docker run -itd -p 2122:2122 --name mycat1cA centos7/mycat1c bash

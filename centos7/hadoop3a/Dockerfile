FROM centos7/hadoop2a
MAINTAINER Wu

#################################
# add hadoop user,set permission for folders.
# setting env var for hadoop user. 
#################################

ENV HADOOP_VERSION=2.9.1
ENV USER_NAME=hadoop


RUN useradd $USER_NAME &&\
	chown -R $USER_NAME /opt/hadoop-${HADOOP_VERSION} &&\
	chgrp -R $USER_NAME /opt/hadoop-${HADOOP_VERSION} &&\	
	echo 'export HADOOP_HOME=/opt/hadoop' | tee -a /home/$USER_NAME/.bashrc &&\
	echo 'export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin' | tee -a /home/$USER_NAME/.bashrc

# docker build --force-rm=true -t centos7/hadoop3a ./


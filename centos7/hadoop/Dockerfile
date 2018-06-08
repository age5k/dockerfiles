FROM centos7/base1
MAINTAINER Wu

# ENV varables.
# ENV http_proxy=http://web-proxy.sgp.hpecorp.net:8080
# ENV https_proxy=http://web-proxy.sgp.hpecorp.net:8080
ENV WORKDIR=/tmp/base1
ENV HADOOP_VERSION=2.9.1
ENV USER_NAME=hadoop

WORKDIR $WORKDIR
#################################
# Download or install packages.
#################################

RUN wget http://www-us.apache.org/dist/hadoop/common/hadoop-${HADOOP_VERSION}/hadoop-${HADOOP_VERSION}.tar.gz

#################################
# Configurations
#################################

# add hadoop user
RUN useradd $USER_NAME

# unzip package and move to hadoop user folder.

RUN tar -xvf $WORKDIR/hadoop-${HADOOP_VERSION}.tar.gz -C $WORKDIR
RUN mkdir /home/$USER_NAME/opt
RUN mv $WORKDIR/hadoop-${HADOOP_VERSION} /home/$USER_NAME/opt
RUN chown -R $USER_NAME /home/$USER_NAME/opt
RUN chgrp -R $USER_NAME /home/$USER_NAME/opt

# symblic link 
RUN ln -s /home/$USER_NAME/opt/hadoop-${HADOOP_VERSION} /home/$USER_NAME/opt/hadoop

# env vars:
RUN echo 'export HADOOP_HOME=~/opt/hadoop' | tee -a /home/$USER_NAME.bashrc
RUN echo 'export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin' | tee -a /home/$USER_NAME/.bashrc

# 
# Configure ssh
#

RUN ssh-keygen -t rsa -P '' -f /home/$USER_NAME/.ssh/id_rsa
RUN cat /home/$USER_NAME/.ssh/id_rsa.pub >> /etc/ssh/authorized_keys


EXPOSE 1-65535

# docker run -itd -p 50010:50010 -p 50020:50020 -p 50075:50075 -p 50090:50090 -p 19888:19888 -p 8030:8030 -p 8031:8031 -p 8032:8032 -p 8033:8033 -p 8040:8040 -p 8042:8042 -p 8088:8088 -p 49707:49707 -p 2122:2122 --name hadoopa centos7/hadoop:2.9.1.ga bash
FROM centos7/base1
MAINTAINER Wu

# ENV varables.
ENV http_proxy=http://web-proxy.sgp.hpecorp.net:8080
ENV https_proxy=http://web-proxy.sgp.hpecorp.net:8080
ENV WORKDIR=/tmp/base1
ENV HADOOP_VERSION=2.9.1
ENV USER_NAME=hadoop

WORKDIR $WORKDIR
# add user
RUN useradd $USER_NAME

# get the tarball.

RUN wget http://www-us.apache.org/dist/hadoop/common/hadoop-${HADOOP_VERSION}/hadoop-${HADOOP_VERSION}.tar.gz

# unzip package
RUN tar -xvf $WORKDIR/hadoop-${HADOOP_VERSION}.tar.gz -C $WORKDIR
RUN mkdir /home/$USER_NAME/opt
RUN move $WORKDIR/hadoop-${HADOOP_VERSION} /home/$USER_NAME/opt
RUN chown -R $USER_NAME /home/$USER_NAME/opt
RUN chgrp -R $USER_NAME /home/$USER_NAME/opt

RUN ln -s /home/$USER_NAME/opt/hadoop-${HADOOP_VERSION} /home/$USER_NAME/opt/hadoop

RUN echo 'export HADOOP_HOME=~/hadoop' | tee -a /home/$USER_NAME_.bashrc
RUN echo 'export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin' | tee -a /home/$USER_NAME/.bashrc

EXPOSE 1-65535
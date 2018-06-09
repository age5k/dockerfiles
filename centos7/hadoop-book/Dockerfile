FROM centos7/hadoop:2.9.1
MAINTAINER Wu

# ENV varables.

ENV WORKDIR=/tmp/base1
ENV HADOOP_VERSION=2.9.1
ENV USER_NAME=hadoop

WORKDIR $WORKDIR
# add user
RUN useradd $USER_NAME

# get the tarball.
RUN mkdir /home/$USER_NAME/git

WORKDIR /home/$USER_NAME/git
RUN get clone https://github.com/tomwhite/hadoop-book.git

WORKDIR /home/$USER_NAME/git/hadoop-book
#
# RUN mvn package -DskipTests
#
RUN echo 'export HADOOP_CLASSPATH=/home/$USER_NAME/git/hadoop-book/hadoop-examples/target/max-temp-workflow/lib/hadoop-examples.jar' | tee -a /home/$USER_NAME/.bashrc
RUN echo 'export HADOOP_CONF_DIR=/home/opt/hadoop/etc/hadoop2' | tee -a /home/$USER_NAME/.bashrc
EXPOSE 1-65535

# docker run -itd -p 50010:50010 -p 50020:50020 -p 50075:50075 -p 50090:50090 -p 19888:19888 -p 8030:8030 -p 8031:8031 -p 8032:8032 -p 8033:8033 -p 8040:8040 -p 8042:8042 -p 8088:8088 -p 49707:49707 -p 2122:2122 --name hadoopa centos7/hadoop-book bash
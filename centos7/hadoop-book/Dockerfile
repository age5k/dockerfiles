FROM centos7/hadoop2c
MAINTAINER Wu

# ENV varables.

ENV WORKDIR=/tmp/wk
ENV HADOOP_VERSION=2.9.1
ENV USER_NAME=hadoop

WORKDIR $WORKDIR
USER $USER_NAME
# get the tarball.
RUN cd  &&\
	mkdir git &&\ 
 	cd git &&\
	git clone https://github.com/tomwhite/hadoop-book.git &&\
	cd hadoop-book &&\
	mvn package -DskipTests

RUN mkdir -p /home/$USER_NAME/opt/hadoop/etc &&\
	cp -R /var/opt/hadoop/etc/hadoop /home/$USER_NAME/opt/hadoop/etc &&\
	chown -R $USER_NAME /home/$USER_NAME/opt &&\
	chgrp -R $USER_NAME /home/$USER_NAME/opt &&\
	echo 'export HADOOP_CONF_DIR=/home/opt/hadoop/etc/hadoop2' | tee -a /home/$USER_NAME/.bashrc &&\ 
	echo 'export HADOOP_CLASSPATH=/home/$USER_NAME/git/hadoop-book/hadoop-examples/target/max-temp-workflow/lib/hadoop-examples.jar' | tee -a /home/$USER_NAME/.bashrc
EXPOSE 1-65535

# docker build --force-rm=true -t centos7/hadoop-book ./
# docker run -itd -p 50010:50010 -p 50020:50020 -p 50075:50075 -p 50090:50090 -p 19888:19888 -p 8030:8030 -p 8031:8031 -p 8032:8032 -p 8033:8033 -p 8040:8040 -p 8042:8042 -p 8088:8088 -p 49707:49707 -p 2122:2122 --name hadoopa centos7/hadoop-book bash
# start-dfs.sh
# start-yarn.sh
# mr-jobhistory-daemon.sh start historyserver
# netstat -nls
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
ADD schema.xml
ADD rule.xml
RUN useradd $USER_NAME &&\
	tar -xvf $WORKDIR/Mycat-server-1.6.5-release-20180122220033-linux.tar.gz -C /opt &&\
	cp postgresql-42.2.2.jar /opt/mycat/lib &&\	
	cp -R /opt/mycat/conf /opt/mycat/conf.orig &&\
	cp schema.xml /opt/mycat/conf &&\
	cp rule.xml /opt/mycat/conf &&\
	chown -R $USER_NAME:$USER_NAME /opt/mycat &&\
	echo 'export MYCAT_HOME=/opt/mycat' | tee -a /home/$USER_NAME/.bashrc &&\
	echo 'export PATH=$PATH:$MYCAT_HOME/bin' | tee -a /home/$USER_NAME/.bashrc


EXPOSE 1-65535
# docker build --force-rm=true -t centos7/mycat1c ./
# docker run -itd -p 9066:9066 -p 8066:8066 --name mycat1cA centos7/mycat1c bash
# mycat start
# mysql -h127.0.0.1 -p123456 -P8066
# connect TESTDB
# create table travelrecord (id bigint not null primary key,user_id varchar(100),traveldate DATE, fee decimal,days int);
# insert into travelrecord(id,user_id,fee,days)values(1,1,1,1);
# see:https://www.jianshu.com/p/39afe8999613
# see: 

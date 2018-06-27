FROM centos7/base2a
MAINTAINER Wu

ENV WORKDIR=/tmp/wk

WORKDIR $WORKDIR
#################################
# Download or install packages.
#################################

RUN wget http://dl.mycat.io/1.6.5/Mycat-server-1.6.5-release-20180122220033-linux.tar.gz &&\
	wget https://jdbc.postgresql.org/download/postgresql-42.2.2.jar
	
RUN yum install -y mysql

# docker build --force-rm=true -t centos7/mycat1a ./
# mycat start
# mysql -h127.0.0.1 -p123456 -P8066
# connect TESTDB
# create table travelrecord (id bigint not null primary key,user_id varchar(100),traveldate DATE, fee decimal,days int);
# insert into travelrecord(id,user_id,fee,days)values(1,1,1,1);
# 
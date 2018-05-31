FROM base1/centos7
MAINTAINER Wu

# ENV varables.
ENV http_proxy=http://web-proxy.sgp.hpecorp.net:8080
ENV https_proxy=http://web-proxy.sgp.hpecorp.net:8080
ENV WORKDIR=/tmp/storm

WORKDIR $WORKDIR
# 
RUN yum install git

# get the tarball.

RUN wget http://www-eu.apache.org/dist/hadoop/common/hadoop-2.9.1/hadoop-2.9.1.tar.gz

RUN wget http://www-eu.apache.org/dist/hive/hive-2.3.3/apache-hive-2.3.3-bin.tar.gz

# get mysql yum repository rpm package.
RUN wget https://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm -P $WORKDIR

# get mysql jdbc driver
RUN wget http://search.maven.org/remotecontent?filepath=mysql/mysql-connector-java/8.0.11/mysql-connector-java-8.0.11.jar mysql-connector-java-8.0.11.jar 

# unzip package
RUN tar -xvf $WORKDIR/hadoop-2.9.1.tar.gz -C $WORKDIR
RUN tar -xvf $WORKDIR/apache-hive-2.3.3-bin.tar.gz -C $WORKDIR

# prepare workdir2
RUN mkdir $WORKDIR2
RUN mv * $WORKDIR2
# hive config
RUN cp $WORKDIR2/apache-hive-2.3.3-bin/conf/hive-default.xml.template $WORKDIR2/apache-hive-2.3.3-bin/conf/hive-site.xml
# # # # # # # # # 
# url:	jdbc:mysql://localhost:3306/hive?createDatabaseIfNotExist=true&useSSL=false
# user:	root
# password:	<![CDATA[iK%<eUQ)#1?p]]>
# driver:	com.mysql.cj.jdbc.Driver
# 
# # # # # # # # # 
RUN chown -R storm $WORKDIR2
RUN chgrp -R storm $WORKDIR2

# install mysql
RUN rpm -ivh mysql57-community-release-el7-9.noarch.rpm
RUN yum -y install mysql-server

# zoo keeper cfg
RUN cp $WORKDIR2/zookeeper-3.4.12/conf/zoo_sample.cfg $WORKDIR2/zookeeper-3.4.12/conf/zoo.cfg 



EXPOSE 1-65535
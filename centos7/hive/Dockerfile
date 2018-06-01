FROM centos7/base1
MAINTAINER Wu

# ENV varables.
ENV http_proxy=http://web-proxy.sgp.hpecorp.net:8080
ENV https_proxy=http://web-proxy.sgp.hpecorp.net:8080
ENV WORKDIR=/tmp/storm

WORKDIR $WORKDIR

# get the tarball.

RUN wget http://www-eu.apache.org/dist/hadoop/common/hadoop-2.9.1/hadoop-2.9.1.tar.gz

RUN wget http://www-eu.apache.org/dist/hive/hive-2.3.3/apache-hive-2.3.3-bin.tar.gz

# get mysql yum repository rpm package.
RUN wget https://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm -P $WORKDIR

# get mysql jdbc driver
RUN wget http://search.maven.org/remotecontent?filepath=mysql/mysql-connector-java/8.0.11/mysql-connector-java-8.0.11.jar

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
# install postgreSQL
RUN yum -y install postgresql-server.x86_64
RUN yum -y install postgresql-jdbc.noarch

# config postgresSQL
RUN mkdir -p /var/run/postgresql/
RUN chown -R storm /var/run/postgresql
RUN ln -s /usr/share/java/postgresql-jdbc.jar $WORKDIR2/apache-hive-2.3.3-bin/lib/postgresql-jdbc.jar
RUN echo 'listen_addresses = \'*\'' > /usr/lib/pgsql/data/postgresql.conf

# env vars:
RUN echo 'export JAVA_HOME=/usr/lib/jvm/java' | tee -a /home/storm/.bashrc

# create folders for hive
RUN mkdir -p /user/hive/warehouse
RUN chown -R storm /user/hive
RUN chgrp -R storm /user/hive

EXPOSE 1-65535

# docker build --force-rm=true -t centos7/hive ./

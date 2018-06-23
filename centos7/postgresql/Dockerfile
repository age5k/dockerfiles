FROM centos7/base2a
MAINTAINER Wu

# ENV varables.

ENV WORKDIR=/tmp/wk

WORKDIR $WORKDIR

# install mysql
RUN yum install -y postgresql-server postgresql-contrib postgresql-jdbc

# config postgresSQL
RUN mkdir -p /var/run/postgresql &&\
	chown -R $USER:$GROUP /var/run/postgresql &&\
	echo 'listen_addresses = \'*\'' > /usr/lib/pgsql/data/postgresql.conf

# setup db
RUN postgresql-setup initdb

EXPOSE 1-65535

# docker build --force-rm=true -t centos7/postgres ./

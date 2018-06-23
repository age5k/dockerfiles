FROM centos7/base2a
MAINTAINER Wu

# ENV varables.

ENV WORKDIR=/tmp/wk

WORKDIR $WORKDIR

# install mysql
RUN yum install -y postgresql-server postgresql-contrib postgresql-jdbc

EXPOSE 1-65535

# docker build --force-rm=true -t centos7/postgres1a ./


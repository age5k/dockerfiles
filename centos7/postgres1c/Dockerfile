FROM centos7/postgres1a
MAINTAINER Wu

# ENV varables.

ENV WORKDIR=/tmp/wk

WORKDIR $WORKDIR

# install postgres

RUN echo 'listen_addresses = \'*\'' > /usr/lib/pgsql/data/postgresql.conf

EXPOSE 1-65535

# docker build --force-rm=true -t centos7/postgres1c ./
# docker run -p 5432:5432 centos7/postgres1c
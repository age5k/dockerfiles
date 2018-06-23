FROM centos7/postgres1a
MAINTAINER Wu

# ENV varables.

ENV WORKDIR=/tmp/wk

WORKDIR $WORKDIR

# install postgres

RUN echo "listen_addresses = \'*\'" >> /var/lib/pgsql/data/postgresql.conf
RUN postgresql-setup initdb
EXPOSE 1-65535

# docker build --force-rm=true -t centos7/postgres1c ./
# docker run -itd -p 5432:5432 --name postgres1cA centos7/postgres1c bash
# docker exec -it postgres1cA bash
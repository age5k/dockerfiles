FROM centos7/postgres2a
MAINTAINER Wu

# ENV varables.

ENV WORKDIR=/tmp/wk

WORKDIR $WORKDIR

##{
# FIX systemctl issue, refer to below pages:
# 	https://github.com/gdraheim/docker-systemctl-replacement
# 	https://blog.centos.org/2015/12/fixing-centos-7-systemd-conflicts-with-docker/
#
ADD systemctl.py $WORKDIR/systemctl.py
RUN mv /usr/bin/systemctl /usr/bin/systemctl.orig &&\
	cp $WORKDIR/systemctl.py /usr/bin/systemctl &&\
	chmod a+x /usr/bin/systemctl
##}

##{ init database,
#   allow any host any user connect even with out a password. Please see:
#		https://www.postgresql.org/docs/9.0/static/auth-pg-hba-conf.html
#   create a test0 db.
#   create a test1 db.


RUN postgresql-setup initdb &&\
	echo "listen_addresses = '*'" >> /var/lib/pgsql/data/postgresql.conf &&\
	echo "host all all 0.0.0.0/0 trust" >> /var/lib/pgsql/data/pg_hba.conf
	systemctl enable postgresql &&\
	systemctl start postgresql &&\
	su - postgres -c "echo 'create database test0' | psql" &&\
	su - postgres -c "echo 'create database test1' | psql"
##}

EXPOSE 1-65535

# docker build --force-rm=true -t centos7/postgres1c ./
# docker run -itd -p 5432:5432 --name postgres1cA centos7/postgres1c bash
# docker exec -it postgres1cA bash
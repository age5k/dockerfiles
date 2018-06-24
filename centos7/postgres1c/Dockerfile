FROM centos7/postgres1a
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

##{ install postgres

RUN postgresql-setup initdb &&\
	echo "listen_addresses = '*'" >> /var/lib/pgsql/data/postgresql.conf &&\
	systemctl enable postgresql
##}

EXPOSE 1-65535

# docker build --force-rm=true -t centos7/postgres1c ./
# docker run -itd -p 5432:5432 --name postgres1cA centos7/postgres1c bash
# docker exec -it postgres1cA bash
FROM centos7/hadoop2a
MAINTAINER Wu

# ENV varables.
# ENV http_proxy=http://web-proxy.sgp.hpecorp.net:8080
# ENV https_proxy=http://web-proxy.sgp.hpecorp.net:8080
ENV WORKDIR=/tmp/wk

WORKDIR $WORKDIR
#################################
# Configurations Step 1,TODO use include in future version of docker.
#################################
######{LANG is missing?
RUN echo 'LANG=en_US.UTF-8' >> /etc/bashrc
######}

######{ START CONFIG ENV vars

# 	Configure JAVA_HOME ENV
RUN echo 'export JAVA_HOME=/usr/lib/jvm/java' | tee -a /etc/profile.d/java.sh &&\
	echo 'export PATH=$PATH:$JAVA_HOME/bin' | tee -a /etc/profile.d/java.sh

######} END CONFIG ENV vars

######{ BEGIN CONFIG sshd

# backup orignal config:
# authroized_keys file reconfigured as a common place. instead of each user's home folder,since centos cannot read them for crepted folder.
RUN cp /etc/ssh/sshd_config /etc/ssh/sshd_config.orig &&\
	sed -ri 's/HostKey \/etc\/ssh\/ssh_host_ecdsa_key/#HostKey \/etc\/ssh\/ssh_host_ecdsa_key/' /etc/ssh/sshd_config &&\
	sed -ri 's/HostKey \/etc\/ssh\/ssh_host_ed25519_key/#HostKey \/etc\/ssh\/ssh_host_ed25519_key/' /etc/ssh/sshd_config &&\
	sed -ri 's/.ssh\/authorized_keys/\/etc\/ssh\/authorized_keys/' /etc/ssh/sshd_config

#generate key pair for root,and for host as the same private key:
RUN ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa &&\
	cat ~/.ssh/id_rsa.pub >> /etc/ssh/authorized_keys &&\
	cp ~/.ssh/id_rsa /etc/ssh/ssh_host_rsa_key

#TODO add service? /user/sbin/sshd
#/usr/sbin/sshd
######} END CONFIG sshd

##{
# FIX systemctl issue, refer to below pages:
# 	https://github.com/gdraheim/docker-systemctl-replacement
# 	https://blog.centos.org/2015/12/fixing-centos-7-systemd-conflicts-with-docker/
#
# ADD systemctl.py $WORKDIR/systemctl.py
# RUN mv /usr/bin/systemctl /usr/bin/systemctl.orig
# RUN cp $WORKDIR/systemctl.py /usr/bin/systemctl
# RUN chmod a+x /usr/bin/systemctl
##}

#################################
# Configurations Step 2
#################################

ENV HADOOP_VERSION=2.9.1
ENV USER_NAME=hadoop

# 
# Configure ssh for user hadoop.
#
RUN mkdir /home/$USER_NAME/.ssh &&\
	ssh-keygen -t rsa -P '' -f /home/$USER_NAME/.ssh/id_rsa &&\
	chown -R $USER_NAME /home/$USER_NAME/.ssh &&\
	chgrp -R $USER_NAME /home/$USER_NAME/.ssh &&\
	cat /home/$USER_NAME/.ssh/id_rsa.pub >> /etc/ssh/authorized_keys
# add hadoop config xml files.	
COPY hadoop hadoop
###
# var for hadoop.
###
RUN mkdir -p /var/opt/hadoop-${HADOOP_VERSION} &&\
	ln -s /var/opt/hadoop-${HADOOP_VERSION} /var/opt/hadoop &&\
	mkdir -p /var/opt/hadoop/etc &&\
	cp -R /opt/hadoop/etc/hadoop /var/opt/hadoop/etc &&\
	cp hadoop/*.* /var/opt/hadoop/etc/hadoop &&\
	chown -R $USER_NAME /var/opt/hadoop &&\
	chgrp -R $USER_NAME /var/opt/hadoop &&\
	echo 'export HADOOP_CONF=/var/opt/hadoop/etc/hadoop' | tee -a /home/$USER_NAME/.bashrc &&\
	echo 'export HADOOP_LOG_DIR=/var/opt/hadoop/logs' | tee -a /home/$USER_NAME/.bashrc

###
# TODO fix 8088 web port issue,see:
# https://stackoverflow.com/questions/23128593/hadoop2-2-0-cant-visit-the-web-http-ip8088
# <property> 
#  <name>yarn.resourcemanager.webapp.address</name>
#  <value>0.0.0.0:8088</value>
# </property>
###
###
# TODO Configurations Step 3,init command,run sshd at start-up.
###
#ADD init.sh /init.sh
#RUN chmod a+x /init.sh
#CMD /init.sh

EXPOSE 1-65535
# docker build --force-rm=true -t centos7/hadoop2c ./
# docker run -itd -p 50010:50010 -p 50020:50020 -p 50075:50075 -p 50090:50090 -p 19888:19888 -p 8030:8030 -p 8031:8031 -p 8032:8032 -p 8033:8033 -p 8040:8040 -p 8042:8042 -p 8088:8088 -p 49707:49707 -p 2122:2122 --name hadoopa centos7/hadoop:2.9.1.ga bash

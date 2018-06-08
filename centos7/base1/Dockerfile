FROM centos:centos7
MAINTAINER Wu

#
# ENV http_proxy=http://web-proxy.sgp.hpecorp.net:8080
# ENV https_proxy=http://web-proxy.sgp.hpecorp.net:8080
ENV WORKDIR=/tmp/base1
RUN mkdir $WORKDIR
WORKDIR $WORKDIR

#################################
#  Download or install packages #
#################################

#install deltarpm
#RUN yum -y install deltarpm

#install wget and get the tarball.
RUN yum -y install wget

# install getopt,ksh

RUN yum -y install util-linux
RUN yum -y install ksh

#? 
RUN yum install -y initscripts

# install necessary common tools?
RUN yum -y install unzip
RUN yum -y install which 
RUN yum -y install openssh-server
RUN yum -y install openssh-clients
RUN yum -y install telnet
RUN yum -y install expect
RUN yum -y install sshpass
RUN yum -y install net-tools

# install dev tools 
RUN yum -y install git
RUN yum -y install maven

# install open jdk
# RUN yum -y install java-1.7.0-openjdk-devel.x86_64
RUN yum -y install java-1.8.0-openjdk java-1.8.0-openjdk-devel 

#################################
# Configurations
#################################

# BEGIN CONFIG sshd
# backup orignal config:
RUN cp /etc/ssh/sshd_config /etc/ssh/sshd_config.orig
#disable key types don't want,remain only rsa:
RUN sed -ri 's/HostKey \/etc\/ssh\/ssh_host_ecdsa_key/#HostKey \/etc\/ssh\/ssh_host_ecdsa_key/' /etc/ssh/sshd_config
RUN sed -ri 's/HostKey \/etc\/ssh\/ssh_host_ed25519_key/#HostKey \/etc\/ssh\/ssh_host_ed25519_key/' /etc/ssh/sshd_config

# make sure public key auth enabled:
#RUN sed -ri '/#PubkeyAuthentication yes/PubkeyAuthentication yes/' /etc/ssh/sshd_config

#authroized_keys file reconfigured as a common place. instead of each user's home folder,since centos cannot read them for crepted folder.
RUN sed -ri '/AuthorizedKeysFile     .ssh\/authorized_keys/AuthorizedKeysFile     \/etc\/ssh\/authorized_keys/' /etc/ssh/sshd_config

#generate key pair:
RUN ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa

#register the pub key for root:
RUN cat ~/.ssh/id_rsa.pub >> /etc/ssh/authorized_keys

#use the key as the host key:
RUN cp ~/.ssh/id_rsa >> /etc/ssh/ssh_host_rsa_key

#TODO add service? /user/sbin/sshd
#/usr/sbin/sshd
# END CONFIG sshd

# START CONFIG ENV vars

# 	Configure JAVA_HOME ENV
RUN echo 'export JAVA_HOME=/usr/lib/jvm/java' | tee -a /etc/profile.d/java.sh
RUN echo 'export PATH=$PATH:$JAVA_HOME/bin' | tee -a /etc/profile.d/java.sh

# 	Configure http proxy
# 	RUN echo 'http_proxy=http://web-proxy.sgp.hpecorp.net:8080' | tee -a /etc/profile.d/http_proxy.sh
# 	RUN echo 'https_proxy=http://web-proxy.sgp.hpecorp.net:8080' | tee -a /etc/profile.d/http_proxy.sh

#LANG is missing?
RUN echo 'LANG=en_US.UTF-8' >> /etc/bashrc

# END CONFIG ENV vars

#docker build --force-rm=true -t centos7/base1 ./

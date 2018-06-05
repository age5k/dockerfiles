FROM centos:centos7
MAINTAINER Wu

#
# ENV http_proxy=http://web-proxy.sgp.hpecorp.net:8080
# ENV https_proxy=http://web-proxy.sgp.hpecorp.net:8080
ENV WORKDIR=/tmp/base1
RUN mkdir $WORKDIR
WORKDIR $WORKDIR

#install deltarpm
RUN yum -y install deltarpm

#install wget and get the tarball.
RUN yum -y install wget

# install getopt,ksh

RUN yum -y install util-linux
RUN yum -y install ksh
# 
RUN yum install -y initscripts

# install open jdk
# RUN yum -y install java-1.7.0-openjdk-devel.x86_64
RUN yum -y install java-1.8.0-openjdk java-1.8.0-openjdk-devel 

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
#
# Configure sshd
#
RUN cp /etc/ssh/sshd_config /etc/ssh/sshd_config.orig
RUN sed -ri 's/HostKey \/etc\/ssh\/ssh_host_ecdsa_key/#HostKey \/etc\/ssh\/ssh_host_ecdsa_key/' /etc/ssh/sshd_config
RUN sed -ri 's/HostKey \/etc\/ssh\/ssh_host_ed25519_key/#HostKey \/etc\/ssh\/ssh_host_ed25519_key/' /etc/ssh/sshd_config
RUN sed -ri '/#PubkeyAuthentication yes/PubkeyAuthentication yes/' /etc/ssh/sshd_config
RUN sed -ri '/AuthorizedKeysFile     .ssh\/authorized_keys/AuthorizedKeysFile     \/etc\/ssh\/authorized_keys/' /etc/ssh/sshd_config

RUN ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
RUN cat ~/.ssh/id_rsa.pub >> /etc/ssh/authorized_keys

########################################
# Configure ENV vars
########################################
# Configure JAVA_HOME ENV
RUN echo 'export JAVA_HOME=/usr/lib/jvm/java' | tee -a /etc/profile.d/java.sh
RUN echo 'export PATH=$PATH:$JAVA_HOME/bin' | tee -a /etc/profile.d/java.sh

# Configure http proxy
# RUN echo 'http_proxy=http://web-proxy.sgp.hpecorp.net:8080' | tee -a /etc/profile.d/http_proxy.sh
# RUN echo 'https_proxy=http://web-proxy.sgp.hpecorp.net:8080' | tee -a /etc/profile.d/http_proxy.sh

#LANG is missing?
RUN echo 'LANG=en_US.UTF-8' >> /etc/bashrc

#docker build --force-rm=true -t centos7/base1 ./

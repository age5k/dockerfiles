FROM centos:centos7
MAINTAINER Wu

#
ENV http_proxy=http://web-proxy.sgp.hpecorp.net:8080
ENV https_proxy=http://web-proxy.sgp.hpecorp.net:8080
ENV WORKDIR=/tmp/storm
RUN mkdir $WORKDIR
WORKDIR $WORKDIR

#install deltarpm
RUN yum -y install deltarpm

#install wget and get the tarball.
RUN yum -y install wget

# install getopt,ksh
# used by install-uca-ebc.sh,so install them in advance.
RUN yum -y install util-linux
RUN yum -y install ksh
# install initscripts for umb zookeeper 
RUN yum install -y initscripts

# install open jdk
RUN yum -y install java-1.7.0-openjdk-devel.x86_64
RUN yum -y install java-1.8.0-openjdk java-1.8.0-openjdk-devel 

# add user storm and wu
RUN useradd storm -s /bin/bash
RUN usermod -a -G wheel storm
RUN useradd wu -s /bin/bash
RUN usermod -a -G wheel wu
# install necessary common tools?
RUN yum -y install unzip
RUN yum -y install which 
RUN yum -y install openssh-clients
RUN yum -y install telnet
RUN yum -y install expect
RUN yum -y install sshpass

#LANG is missing?
RUN echo 'LANG=en_US.UTF-8' >> /etc/bashrc

#docker build --force-rm=true -t base1/centos7 ./
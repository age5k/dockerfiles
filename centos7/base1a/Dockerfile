FROM centos:centos7
MAINTAINER Wu

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

#docker build --force-rm=true -t centos7/base1a ./
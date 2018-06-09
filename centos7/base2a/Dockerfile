FROM centos7/base1a
MAINTAINER Wu

#################################
#  Download or install packages #
#################################

# install dev tools 
RUN yum -y install git
RUN yum -y install maven

# install open jdk
RUN yum -y install java-1.7.0-openjdk-devel
RUN yum -y install java-1.8.0-openjdk java-1.8.0-openjdk-devel 
#docker build --force-rm=true -t centos7/base2a ./
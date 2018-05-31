FROM base1/centos7
MAINTAINER Wu

# ENV varables.
ENV http_proxy=http://web-proxy.sgp.hpecorp.net:8080
ENV https_proxy=http://web-proxy.sgp.hpecorp.net:8080
ENV WORKDIR=/tmp/storm
ENV WORKDIR2=/home/storm/tmp
WORKDIR $WORKDIR
# 
RUN yum install git

# get the tarball.

RUN wget http://www-us.apache.org/dist/zookeeper/zookeeper-3.4.12/zookeeper-3.4.12.tar.gz -P $WORKDIR
RUN wget http://www-us.apache.org/dist/kafka/1.1.0/kafka_2.11-1.1.0.tgz -P $WORKDIR
RUN wget http://www.igniterealtime.org/downloadServlet?filename=openfire/openfire_4_2_3.tar.gz -P $WORKDIR
# unzip the tarball
RUN tar -xvf $WORKDIR/zookeeper-3.4.12.tar.gz -C $WORKDIR
RUN tar -xvf $WORKDIR/kafka_2.11-1.1.0.tgz -C $WORKDIR
RUN tar -xvf $WORKDIR/downloadServlet?filename=openfire%2Fopenfire_4_2_3.tar.gz

# prepare workdir2
RUN mkdir $WORKDIR2
RUN mv * $WORKDIR2

# zoo keeper cfg
RUN cp $WORKDIR2/zookeeper-3.4.12/conf/zoo_sample.cfg $WORKDIR2/zookeeper-3.4.12/conf/zoo.cfg 

# owner to storm user
RUN chown -R storm $WORKDIR2
RUN chgrp -R storm $WORKDIR2

# setting .bashrc
RUN echo 'export PATH=$WORKDIR2/zookeeper-3.4.12/bin:$PATH' | tee -a /home/storm/.bashrc
RUN echo 'export PATH=$WORKDIR2/kafka_2.11-1.1.0/bin:$PATH' | tee -a /home/storm/.bashrc
RUN echo 'export PATH=$WORKDIR2/openfire/bin:$PATH' | tee -a /home/storm/.bashrc

# prepare the start command 
RUN echo 'zkServer.sh start' | tee -a /home/storm/readme.txt
RUN echo 'nohup kafka-server-start.sh $WORKDIR2/kafka_2.11-1.1.0/config/server.properties &' | tee -a /home/storm/readme.txt
RUN echo 'zkServer.sh start' | tee -a /home/storm/readme.txt

EXPOSE 1-65535
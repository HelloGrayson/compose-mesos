FROM jpetazzo/dind
MAINTAINER breerly

RUN echo "deb http://repos.mesosphere.io/ubuntu/ trusty main" > /etc/apt/sources.list.d/mesosphere.list
RUN apt-key adv --keyserver keyserver.ubuntu.com --recv E56151BF

RUN apt-get -y update

RUN apt-get -y install mesos=0.20.1-1.0.ubuntu1404

# for slave
RUN apt-get -y install supervisor
ADD supervisord.conf /etc/supervisor/supervisord.conf

ADD slave.sh /slave.sh
RUN chmod +x /slave.sh

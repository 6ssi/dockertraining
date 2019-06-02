#FROM jenkins:1.609.3
FROM jenkins:latest

USER root
RUN echo "Acquire::Check-Valid-Until \"faLse\";" >> /etc/apt/apt.conf.d/70debconf && echo "deb http://httpredir.debian.org/debian jessie main" > /etc/apt/sources.list && echo "deb http://security.debian.org jessie/updates main" >> /etc/apt/sources.list && echo "deb http://archive.debian.org/debian-archive/debian jessie-backports main" > /etc/apt/sources.list.d/jessie-backports.list && echo "deb http://apt.dockerproject.org/repo debian-jessie main" > /etc/apt/sources.list.d/docker.list && apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D && apt-get update && apt-get install -y apt-transport-https && apt-get install -y sudo && apt-get install -y docker-engine && rm -rf /var/lib/apt/lists/*
RUN echo "jenkins ALL=NOPASSWD: ALL " >> /etc/sudoers

RUN curl -L https://github.com/docker/compose/releases/download/1.4.1/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose; chmod +x /usr/local/bin/docker-compose

USER jenkins
COPY plugins.txt /usr/share/jenkins/plugins.txt
RUN /usr/local/bin/plugins.sh /usr/share/jenkins/plugins.txt

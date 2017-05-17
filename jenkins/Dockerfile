# version 0.0.1
FROM ubuntu:14.04
MAINTAINER achar "zuolifeng@sina.com"
ENV REFRESHED_AT 2017-05-15

# 修改软件源到阿里云镜像
RUN cp /etc/apt/sources.list /etc/apt/sources.list.bak
RUN echo "# Change the source to Aliyun.com" > /etc/apt/sources.list
RUN echo "deb http://mirrors.aliyun.com/ubuntu/ trusty main restricted universe multiverse" >> /etc/apt/sources.list
RUN echo "deb http://mirrors.aliyun.com/ubuntu/ trusty-security main restricted universe multiverse" >> /etc/apt/sources.list
RUN echo "deb http://mirrors.aliyun.com/ubuntu/ trusty-updates main restricted universe multiverse" >> /etc/apt/sources.list
RUN echo "deb http://mirrors.aliyun.com/ubuntu/ trusty-proposed main restricted universe multiverse" >> /etc/apt/sources.list
RUN echo "deb http://mirrors.aliyun.com/ubuntu/ trusty-backports main restricted universe multiverse" >> /etc/apt/sources.list
RUN echo "deb-src http://mirrors.aliyun.com/ubuntu/ trusty main restricted universe multiverse" >> /etc/apt/sources.list
RUN echo "deb-src http://mirrors.aliyun.com/ubuntu/ trusty-security main restricted universe multiverse" >> /etc/apt/sources.list
RUN echo "deb-src http://mirrors.aliyun.com/ubuntu/ trusty-updates main restricted universe multiverse" >> /etc/apt/sources.list
RUN echo "deb-src http://mirrors.aliyun.com/ubuntu/ trusty-proposed main restricted universe multiverse" >> /etc/apt/sources.list
RUN echo "deb-src http://mirrors.aliyun.com/ubuntu/ trusty-backports main restricted universe multiverse" >> /etc/apt/sources.list

# 开始更新服务器
RUN apt-get -yqq update
RUN apt-get -yqq install curl apt-transport-https
RUN apt-key adv --keyserver hkp://pgp.mit.edu:80 --recv-keys 58118E89F3A912897C070ADBF76221572C52609D
RUN echo deb https://apt.dockerproject.org/repo ubuntu-trusty main > /etc/apt/sources.list.d/docker.list
RUN apt-get update -yqq
RUN apt-get install -yqq iptables  openjdk-7-jdk git-core docker-engine

# 设置jenkins环境
ENV JENKINS_BASE /jenkins
ENV JENKINS_HOME $JENKINS_BASE/data
ENV JENKINS_MIRROR http://mirrors.jenkins-ci.org


# 配置jenkins
#http://mirrors.jenkins-ci.org/war-stable/latest/jenkins.war

RUN mkdir -p $JENKINS_HOME/plugins
RUN curl -sf -o $JENKINS_BASE/jenkins.war -L $JENKINS_MIRROR/war-stable/latest/jenkins.war

RUN for plugin in chucknorris greenballs scm-api git-client git ws-cleanup;\
do \
   curl -sf -o $JENKINS_HOME/plugins/${plugin}.hpi \
  -L $JENKINS_MIRROR/plugins/${plugin}/latest/${plugin}.hpi; \
done 

ADD ./dockerjenkins.sh /usr/local/bin/dockerjenkins.sh
RUN chmod +x /usr/local/bin/dockerjenkins.sh

VOLUME /var/lib/docker

# 开放端口映射
EXPOSE 8080

# 运行
ENTRYPOINT ["/usr/local/bin/dockerjenkins.sh"]




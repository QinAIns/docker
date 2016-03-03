FROM alpine:latest

MAINTAINER qinains <qinains@qq.com>

ENV JENKINS_HOME /var/lib/jenkins
ENV JENKINS_LOG /var/log/jenkins
ENV PATH $PATH:/usr/lib/jvm/default-jvm/bin
EXPOSE 8080 50000

RUN apk --no-cache add openjdk8 ttf-dejavu openssh git

RUN adduser -D -h $JENKINS_HOME jenkins \
&& mkdir $JENKINS_LOG && chown -R jenkins:jenkins $JENKINS_LOG \
&& su jenkins -c "mkdir -p $JENKINS_HOME/.jenkins/war" \
&& cd $JENKINS_HOME/.jenkins/war \
&& wget http://mirrors.jenkins-ci.org/war-stable/latest/jenkins.war

WORKDIR $JENKINS_HOME/.jenkins/war
RUN su jenkins -c "jar -xvf jenkins.war" \
&& rm jenkins.war

VOLUME ["$JENKINS_HOME", "$JENKINS_LOG"]

ENTRYPOINT su jenkins -c "java -jar $JENKINS_HOME/.jenkins/war/winstone.jar --webroot=$JENKINS_HOME/.jenkins/war"

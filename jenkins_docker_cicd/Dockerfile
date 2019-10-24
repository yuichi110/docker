From jenkins/jenkins:2.190.1-centos

USER root
RUN yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
RUN yum install -y yum-utils device-mapper-persistent-data lvm2 docker-ce-cli 
RUN curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
RUN chmod +x /usr/local/bin/docker-compose

RUN mkdir /var/jenkins_home/.ssh; chown jenkins:jenkins /var/jenkins_home/.ssh
COPY --chown=jenkins:jenkins ./id_rsa /var/jenkins_home/.ssh/id_rsa
COPY --chown=jenkins:jenkins ./id_rsa.pub /var/jenkins_home/.ssh/id_rsa.pub
COPY --chown=jenkins:jenkins ./ssh_config /var/jenkins_home/.ssh/config

Expose 8080
Expose 50000
ENV JAVA_OPTS -Djava.awt.headless=true -Dorg.apache.commons.jelly.tags.fmt.timeZone=Asia/Tokyo -Dfile.encoding=UTF-8 -Dsun.jnu.encoding=UTF-8

USER jenkins
ENTRYPOINT ["/sbin/tini", "--", "/usr/local/bin/jenkins.sh"]
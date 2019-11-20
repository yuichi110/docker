From jenkins/jenkins:2.190.1-centos

USER root
RUN yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
RUN yum install -y yum-utils device-mapper-persistent-data lvm2 docker-ce-cli 
RUN curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
RUN chmod +x /usr/local/bin/docker-compose
COPY --chown=jenkins:jenkins ./id_rsa /tmp/id_rsa
COPY --chown=jenkins:jenkins ./id_rsa.pub /tmp/id_rsa.pub
COPY --chown=jenkins:jenkins ./ssh_config /tmp/config
COPY ./jenkins.sh /usr/local/bin/jenkins.sh
RUN chmod 0775 /usr/local/bin/jenkins.sh
Expose 8080
Expose 50000

USER jenkins
ENV JAVA_OPTS -Djava.awt.headless=true -Dorg.apache.commons.jelly.tags.fmt.timeZone=Asia/Tokyo -Dfile.encoding=UTF-8 -Dsun.jnu.encoding=UTF-8
ENTRYPOINT ["/sbin/tini", "--", "/usr/local/bin/jenkins.sh"]
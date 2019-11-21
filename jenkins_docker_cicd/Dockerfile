From jenkins/jenkins:2.190.1-centos

USER root
COPY --chown=jenkins:jenkins ./id_rsa /tmp/id_rsa
COPY --chown=jenkins:jenkins ./id_rsa.pub /tmp/id_rsa.pub
COPY ./jenkins.sh /usr/local/bin/jenkins.sh
RUN chmod 0600 /tmp/id_rsa \
    && chmod 0600 /tmp/id_rsa.pub \
    && chmod 0775 /usr/local/bin/jenkins.sh
    && yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo \
    && yum install -y yum-utils device-mapper-persistent-data lvm2 docker-ce-cli \
    && curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose \
    && chmod +x /usr/local/bin/docker-compose \
    && rm -rf /var/cache/yum/* \
    && yum clean all
Expose 8080
Expose 50000

USER jenkins
ENV JAVA_OPTS -Djava.awt.headless=true -Dorg.apache.commons.jelly.tags.fmt.timeZone=Asia/Tokyo -Dfile.encoding=UTF-8 -Dsun.jnu.encoding=UTF-8
ENTRYPOINT ["/sbin/tini", "--", "/usr/local/bin/jenkins.sh"]
FROM registry.access.redhat.com/openshift3/jenkins-slave-base-rhel7

LABEL com.redhat.component="jenkins-slave-zap" \
      name="jenkins-slave-zap" \
      architecture="x86_64" \
      io.k8s.display-name="Jenkins Slave Image Management" \
      io.k8s.description="Jenkins slave base image - zap" \
      io.openshift.tags="openshift,jenkins,slave,zap"
USER root

ENV LC_ALL en_US.utf-8
ENV LANG en_US.utf-8
ENV ZAP_PATH /opt/zaproxy

WORKDIR /tmp

RUN yum repolist > /dev/null && \
    yum clean all && \
    yum -y install fontconfig && \
     yum install -y --enablerepo=rhel-server-rhscl-7-rpms --setopt=tsflags=nodocs rh-python36 && \
    curl --location https://github.com/zaproxy/zaproxy/releases/download/v2.8.0/ZAP_2_8_0_unix.sh --output /zap.sh && \
    chmod 700  /zap.sh && \
    printf "o\n\n\n\n\n\n\n\n\n1\n1\n" | /zap.sh && \
    scl enable rh-python36 "python3 -m pip install --upgrade zapcli" && \
    rm -f /zap.sh && \
    ln -s /opt/rh/rh-python36/root/usr/bin/zap-cli /usr/bin/zap-cli && \
    ln -s /tmp/zap.log /opt/zaproxy/zap.log && \
    ln -s /tmp /.ZAP && \
    yum clean all

USER 1001


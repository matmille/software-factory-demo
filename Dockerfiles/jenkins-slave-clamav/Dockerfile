FROM registry.access.redhat.com/openshift3/jenkins-slave-base-rhel7

LABEL com.redhat.component="jenkins-slave-clamav" \
      name="jenkins-slave-clamav" \
      architecture="x86_64" \
      io.k8s.display-name="Jenkins Slave Image Management" \
      io.k8s.description="Jenkins slave base image - clamav" \
      io.openshift.tags="openshift,jenkins,slave,clamav"
USER root

RUN yum repolist > /dev/null && \
    yum clean all && \
    yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && \
    yum install -y --setopt=tsflags=nodocs clamav && \
    freshclam && \
    yum clean all

USER 1001


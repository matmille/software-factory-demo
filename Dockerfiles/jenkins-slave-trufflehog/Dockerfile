FROM registry.access.redhat.com/openshift3/jenkins-slave-base-rhel7

LABEL com.redhat.component="jenkins-slave-trufflehog" \
      name="jenkins-slave-trufflehog" \
      architecture="x86_64" \
      io.k8s.display-name="Jenkins Slave Image Management" \
      io.k8s.description="Jenkins slave base image - trufflehog" \
      io.openshift.tags="openshift,jenkins,slave,trufflehog"
USER root

RUN yum repolist > /dev/null && \
    yum clean all && \
    yum install -y --enablerepo=rhel-server-rhscl-7-rpms --setopt=tsflags=nodocs rh-python36 && \
    yum clean all && \
    scl enable rh-python36 python3 -m pip install trufflehog

USER 1001


FROM registry.access.redhat.com/openshift3/jenkins-slave-base-rhel7

LABEL com.redhat.component="jenkins-slave-skopeo" \
      name="jenkins-slave-skopeo" \
      architecture="x86_64" \
      io.k8s.display-name="Jenkins Slave Image Management" \
      io.k8s.description="Jenkins slave base image - skopeo" \
      io.openshift.tags="openshift,jenkins,slave,skopeo"
USER root

RUN yum repolist > /dev/null && \
    yum clean all && \
    yum install -y --enablerepo=rhel-7-server-extras-rpms --setopt=tsflags=nodocs skopeo && \
    yum clean all

USER 1001

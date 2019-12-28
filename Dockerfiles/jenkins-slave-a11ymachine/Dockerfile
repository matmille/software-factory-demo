FROM registry.access.redhat.com/openshift3/jenkins-slave-base-rhel7

LABEL com.redhat.component="jenkins-slave-a11ymachine" \
      name="jenkins-slave-a11ymachine" \
      architecture="x86_64" \
      io.k8s.display-name="Jenkins Slave Image Management" \
      io.k8s.description="Jenkins slave base image - a11ymachine" \
      io.openshift.tags="openshift,jenkins,slave,a11ymachine"
USER root

RUN yum repolist > /dev/null && \
    yum clean all && \
    yum install -y --enablerepo=rhel-server-rhscl-7-rpms --setopt=tsflags=nodocs bzip2 rh-nodejs6 && \
    yum clean all && \
    scl enable rh-nodejs6 "NPM_CONFIG_LOGLEVEL=warn NPM_CONFIG_PROGRESS=false NPM_CONFIG_SPIN=false npm install -g the-a11y-machine" && \
    ln -s /tmp /a11ym_output

# Enable rh-nodejs6 
RUN printf '#!/bin/bash\nsource scl_source enable rh-nodejs6\nexec "$@"\n' > /usr/bin/entrypoint.sh && \
    chmod +x /usr/bin/entrypoint.sh

ENTRYPOINT [ "/usr/bin/entrypoint.sh" ]

USER 1001


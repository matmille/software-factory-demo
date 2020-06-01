FROM dev-user50/eap73-openjdk11-openshift-rhel8:latest

LABEL com.redhat.component="eap73-openshift-hardened" \
      name="eap73-openshift-hardened" \
      architecture="x86_64" \
      io.k8s.display-name="EAP 7.3 Hardened Image" \
      io.k8s.description="Remove fangs and update image" \
      io.openshift.tags="openshift,eap"
USER root

RUN yum repolist > /dev/null && \
    yum clean all && \
    yum -y update && \
    yum clean all
RUN find / -xdev -perm /6000 -type f -exec chmod a-s {} \;

USER 1001

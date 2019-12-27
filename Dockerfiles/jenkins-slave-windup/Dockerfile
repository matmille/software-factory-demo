FROM registry.access.redhat.com/openshift3/jenkins-slave-base-rhel7

LABEL com.redhat.component="jenkins-slave-windup" \
      name="jenkins-slave-windup" \
      architecture="x86_64" \
      io.k8s.display-name="Jenkins Slave Image Management" \
      io.k8s.description="Jenkins slave base image - windup" \
      io.openshift.tags="openshift,jenkins,slave,windup"
USER root

RUN yum repolist > /dev/null && \
    yum clean all && \
    yum install -y --enablerepo=rhel-server-rhscl-7-rpms --setopt=tsflags=nodocs rh-maven36 rh-maven36-xmvn-connector-aether && \
    yum clean all && \
    git clone https://github.com/windup/windup.git && \
    git clone  https://github.com/windup/windup-rulesets.git && \
    git clone https://github.com/windup/windup-distribution && \
    scl enable rh-maven36 "cd /windup;mvn clean install -DskipTests" && \
    scl enable rh-maven36 "cd /windup-rulesets;mvn clean install -DskipTests" && \
    scl enable rh-maven36 "cd /windup-distribution;mvn clean install -DskipTests" && \
    mv /windup-distribution/target/rhamt*zip / && \
    rm -rf /root/.m2 /windup /windup-rulesets /windup-distribution && \
    unzip /rhamt*zip && \
    rm -f /rhamt*zip && \
    ln -s /rhamt* /rhamt && \
    mkdir /.rhamt && \
    chmod 755 /.rhamt && \
    ln -s /tmp /.rhamt/log

ENV JAVA_HOME /usr/lib/jvm/java
ENV PATH $JAVA_HOME/bin:$PATH:/rhamt/bin

USER 1001


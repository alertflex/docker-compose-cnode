FROM payara/server-full:5.2020.5
MAINTAINER alertflex

# User supplied inputs
USER payara

ARG ADMIN_PWD

COPY post-boot-commands.asadmin /opt/payara/config/post-boot-commands.asadmin
RUN sed -i "s/_admin_pwd/${ADMIN_PWD}/g" "/opt/payara/config/post-boot-commands.asadmin"
RUN mkdir -p /opt/payara/alertflex/
USER root
RUN apt-get update && apt-get install -y wget && \
    mkdir -p /opt/payara/alertflex/ && \
    mkdir -p /opt/payara/appserver/glassfish/domains/production/lib/ext/ && \
    wget -O /opt/payara/alertflex/alertflex-ctrl.war https://github.com/alertflex/cnode/releases/download/v1.0.5/alertflex-ctrl.war && \
    wget -O /opt/payara/alertflex/activemq-rar-5.16.1.rar https://repo1.maven.org/maven2/org/apache/activemq/activemq-rar/5.16.1/activemq-rar-5.16.1.rar && \
    wget -O /opt/payara/appserver/glassfish/domains/production/lib/ext/mysql-connector-java-5.1.35.jar https://repo1.maven.org/maven2/mysql/mysql-connector-java/5.1.35/mysql-connector-java-5.1.35.jar
USER payara

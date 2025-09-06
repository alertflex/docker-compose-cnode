FROM openjdk:8-jre

ARG ADMIN_PWD

# set env
ENV ACTIVEMQ_VERSION=5.16.1 \
    ACTIVEMQ=apache-activemq-5.16.1 \
    ACTIVEMQ_TCP=61616 \
    ACTIVEMQ_UI=8161 \
    ACTIVEMQ_HOME=/opt/activemq

# set activeMQ
RUN curl -f "https://archive.apache.org/dist/activemq/${ACTIVEMQ_VERSION}/${ACTIVEMQ}-bin.tar.gz" -o "${ACTIVEMQ}-bin.tar.gz" && \
    tar xzf "${ACTIVEMQ}-bin.tar.gz" -C /opt && \
    ln -s "/opt/${ACTIVEMQ}" "${ACTIVEMQ_HOME}" && \
    rm "${ACTIVEMQ}-bin.tar.gz" && \
    rm -rf "${ACTIVEMQ_HOME}/examples" && \
    rm -rf "${ACTIVEMQ_HOME}/docs" && \
    useradd -r -M -d "${ACTIVEMQ_HOME}" activemq && \
    chown -R activemq:activemq "/opt/${ACTIVEMQ}" && \
    chown -h activemq:activemq "${ACTIVEMQ_HOME}" && \
    chmod 755 "${ACTIVEMQ_HOME}"

# copy configs
COPY activemq.xml "${ACTIVEMQ_HOME}/conf/"
COPY jetty-realm.properties "${ACTIVEMQ_HOME}/conf/"

RUN sed -i "s/_admin_pwd/${ADMIN_PWD}/g" "${ACTIVEMQ_HOME}/conf/activemq.xml" && \
    sed -i "s/_admin_pwd/${ADMIN_PWD}/g" "${ACTIVEMQ_HOME}/conf/jetty-realm.properties"

# set rights
RUN chown activemq:activemq "${ACTIVEMQ_HOME}/conf/activemq.xml" \
    "${ACTIVEMQ_HOME}/conf/jetty-realm.properties"

USER activemq

WORKDIR "${ACTIVEMQ_HOME}"
EXPOSE ${ACTIVEMQ_TCP} ${ACTIVEMQ_UI}

CMD ["/bin/sh", "-c", "bin/activemq console"]

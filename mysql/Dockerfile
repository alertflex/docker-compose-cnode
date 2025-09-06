FROM mysql:5.7.42

ARG ADMIN_PWD
ARG PROJECT_ID

COPY init.sql /docker-entrypoint-initdb.d/
COPY mysqld.cnf /etc/mysql/mysql.conf.d/mysqld.cnf

RUN sed -i "s/_admin_pwd/${ADMIN_PWD}/g" /docker-entrypoint-initdb.d/init.sql && \
    sed -i "s/_project_id/${PROJECT_ID}/g" /docker-entrypoint-initdb.d/init.sql && \
	sed -i "s|_os_url|${OPENSEARCH_URL}|g" /docker-entrypoint-initdb.d/init.sql && \
	sed -i "s/_os_port/${OPENSEARCH_PORT}/g" /docker-entrypoint-initdb.d/init.sql && \
	sed -i "s/_os_user/${OPENSEARCH_USER}/g" /docker-entrypoint-initdb.d/init.sql && \
	sed -i "s/_os_pwd/${OPENSEARCH_PWD}/g" /docker-entrypoint-initdb.d/init.sql

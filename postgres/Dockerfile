FROM postgres:13.1


ENV PGDATA /var/lib/postgresql/data/pgdata
ENV POSTGRES_USER postgres
ENV POSTGRES_PASSWORD postgres
ENV POSTGRES_DB postgres

ADD 01-postgres-init.sql  /docker-entrypoint-initdb.d/
ADD 02-hive-schema-2.3.7.postgres.sql  /docker-entrypoint-initdb.d/
ADD 03-hive-txn-schema-2.3.7.postgres.sql  /docker-entrypoint-initdb.d/

HEALTHCHECK CMD pg_isready -U ${POSTGRES_USER} -d ${POSTGRES_DB} || exit 1
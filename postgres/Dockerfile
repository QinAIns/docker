FROM alpine:latest

MAINTAINER qinains <qinains@qq.com>

ENV LANG en_US.utf8
ENV PGHOME /var/lib/postgresql/
ENV PGDATA /var/lib/postgresql/data/
ENV PGLOG /var/log/postgresql/
VOLUME ["$PGHOME", "$PGDATA", "$PGLOG"]
EXPOSE 5432

RUN apk --no-cache add postgresql postgresql-client postgresql-contrib

ENTRYPOINT if [ ! -s "$PGDATA/PG_VERSION" ]; then ( \
chown -R postgres:postgres $PGHOME \
&& chown -R postgres:postgres $PGDATA \
&& chown -R postgres:postgres $PGLOG \
&& su postgres -c "initdb --encoding=UTF8 --pgdata='$PGDATA'" \
&& su postgres -c "echo \"ALTER USER postgres WITH SUPERUSER PASSWORD 'postgres';\" | postgres --single -jE" \
&& sed -ri "s/^#(listen_addresses\s*=\s*)\S+/\1'*'/" $PGDATA/postgresql.conf \
&& sed -ri "s/^#(max_connections\s*=\s*)\S+/\1256/" $PGDATA/postgresql.conf \
&& sed -ri "s/^#(log_min_duration_statement\s*=\s*)\S+/\1500/" $PGDATA/postgresql.conf \
&& echo "host all all 0.0.0.0/0 md5" >> $PGDATA/pg_hba.conf \
)fi \
&& su postgres -c "postgres"

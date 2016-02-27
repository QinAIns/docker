FROM alpine:latest

MAINTAINER qinains <qinains@qq.com>

ENV LANG en_US.utf8
ENV PGHOME /var/lib/postgresql/
ENV PGDATA /var/lib/postgresql/data
VOLUME [$PGHOME,$PGDATA]
EXPOSE 5432

RUN apk --no-cache add postgresql postgresql-client postgresql-contrib
#chrony

ENTRYPOINT if [ ! -s "$PGDATA/PG_VERSION" ]; then ( \
chown -R postgres:postgres $PGHOME \
&& chown -R postgres:postgres $PGDATA \
&& su postgres -c "initdb --encoding=UTF8 --pgdata='$PGDATA'" \
&& su postgres -c "echo \"ALTER USER postgres WITH SUPERUSER PASSWORD 'postgres';\" | postgres --single -jE" \
&& sed -ri "s/^#(listen_addresses\s*=\s*)\S+/\1'*'/" $PGDATA/postgresql.conf \
&& echo "host all all 0.0.0.0/0 md5" >> $PGDATA/pg_hba.conf \
)fi; \
su postgres -c "postgres"

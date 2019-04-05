FROM centos:latest AS binarybuild

ARG postgres_user=postgres
ARG postgres_password
ARG pgsql_prefix=/pgsql
RUN yum clean all
#RUN yum -y update && yum -y upgrade && yum clean all

COPY ./pgsql ${pgsql_prefix}
RUN mkdir -p ${pgsql_prefix}/backups ${pgsql_prefix}/data ${pgsql_prefix}/log
RUN groupadd -r ${postgres_user} \
    && useradd -d ${pgsql_prefix} -g ${postgres_user} -r ${postgres_user} \
    && echo "${postgres_user}:${postgres_password}" | chpasswd \
    && chown -R postgres:postgres ${pgsql_prefix}
#RUN echo "postgres:${postgres_password}" | chpasswd


USER postgres
RUN echo "${postgres_password}" > ${pgsql_prefix}/passfile \
    && ${pgsql_prefix}/bin/initdb -D ${pgsql_prefix}/data/ -U postgres --pwfile=${pgsql_prefix}/passfile --encoding='UTF-8' --locale='en_US.UTF-8' \
    && rm -f /pgsql/passfile
COPY --chown=postgres:postgres ./pg_hba.conf ${pgsql_prefix}/data/pg_hba.conf
COPY --chown=postgres:postgres ./postgresql.conf ${pgsql_prefix}/postgresql.conf

FROM minix:latest
COPY --from=binarybuild ${pgsql_prefix} ${pgsql_prefix}

EXPOSE 5432
#CMD ["-D", "${pgsql_prefix}/data/", "-l", "${pgsql_prefix}/log/start.log", "start"]
#ENTRYPOINT ["${pgsql_prefix}/bin/pg_ctl"]
ENTRYPOINT ["/bin/bash"]

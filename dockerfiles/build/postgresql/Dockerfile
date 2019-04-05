FROM centos:latest

ARG pg_version
ARG build_path

RUN yum -y update && yum -y upgrade \
    && yum -y install wget make gcc perl flex bison \
    zlib-devel readline-devel openssl-devel pam-devel openldap-devel \
    && yum clean all

ADD *.tar.gz /tmp
RUN rm -f /tmp/*.tar.gz

WORKDIR /tmp/postgresql-${pg_version}
RUN ./configure --prefix=${build_path} \
    --with-openssl --with-ldap --with-pam \
    && make && make install

FROM centos:latest

ARG package_name=bash
ARG package_version=5.0
ARG package=${package_name}-${package_version}
ARG build_path
ARG gnu_ftp_base_uri=ftp://ftp.gnu.org/gnu
ARG gnu_patches_uri=${gnu_ftp_base_uri}/${package_name}/${package}-patches

RUN yum -y update && yum -y upgrade \
    && yum -y install wget glibc-static patch make gcc \
    && yum clean all

WORKDIR /tmp
RUN wget ${gnu_ftp_base_uri}/${package_name}/${package}.tar.gz \
    && tar xzf ${package}.tar.gz \
    && rm -f ${package}.tar.gz
RUN mkdir -p ${package}-patches \
    && wget -P ${package}-patches ${gnu_patches_uri}/bash50-001 \
    && wget -P ${package}-patches ${gnu_patches_uri}/bash50-002 \
    && wget -P ${package}-patches ${gnu_patches_uri}/bash50-003

RUN patch -p0 -d/tmp/bash-5.0 < bash50-003

#WORKDIR /tmp/bash-${bash_version}
#RUN ./configure --prefix=${build_path} --enable-minimal-config --enable-array-variables --enable-debugger --enable-help-builtin --enable-history --enable-readline --enable-strict-posix-default --enable-static-link && make && make install

ENTRYPOINT ["/bin/bash"]

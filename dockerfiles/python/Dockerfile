FROM centos:latest
ARG python_version=3.7.3
RUN yum -y update && yum -y upgrade \
    && yum -y install wget make gcc zlib-devel openssl-devel \
    && yum clean all
COPY download_python download_python
RUN ./download_python ${python_version}
#ADD rootfs.tar.gz /
ENTRYPOINT ["/bin/bash"]

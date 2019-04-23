FROM centos:latest
RUN yum -y update && yum -y upgrade \
    && yum -y install make gcc libffi-devel zlib-devel openssl-devel \
    && yum clean all
ADD Python-*.xz .
ENTRYPOINT ["/bin/bash"]

FROM gcc:centos-8
MAINTAINER sconstantino@grupobme.es
ARG num_cores
WORKDIR /tmp
ADD Python-3.7.4.tar.xz ./
WORKDIR /tmp/Python-3.7.4
RUN ./configure --enable-optimizations --enable-shared --with-lto
RUN make -j${num_cores}
# Optional:
#RUN make -j${num_cores} test
RUN make install
RUN ldconfig
RUN pip3 install --upgrade pip
RUN pip3 install --upgrade setuptools

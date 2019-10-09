FROM centos:8-devtools
MAINTAINER sconstantino@grupobme.es

ARG num_cores

# LD config
RUN echo /usr/local/lib > /etc/ld.so.conf.d/libc.conf
RUN echo /usr/local/lib64 >> /etc/ld.so.conf.d/libc.conf

# DejaGnu 1.6.2
WORKDIR /tmp
ADD dejagnu-1.6.2.tar.gz ./
WORKDIR /tmp/dejagnu-1.6.2
RUN ./configure
RUN make -j${num_cores}
RUN make -j${num_cores} check
RUN make install

# GMP 6.1.2
WORKDIR /tmp
ADD gmp-6.1.2.tar.xz ./
WORKDIR /tmp/gmp-6.1.2
RUN ./configure --enable-cxx
RUN make -j${num_cores}
RUN make -j${num_cores} check
RUN make install
RUN ldconfig

# MPFR 4.0.2
WORKDIR /tmp
ADD mpfr-4.0.2.tar.xz ./
WORKDIR /tmp/mpfr-4.0.2
RUN ./configure
RUN make -j${num_cores}
RUN make -j${num_cores} check
RUN make -j${num_cores} check-gmp-symbols
RUN make install
RUN ldconfig

# MPC 1.1.0
WORKDIR /tmp
ADD mpc-1.1.0.tar.gz ./
WORKDIR /tmp/mpc-1.1.0
RUN ./configure
RUN make -j${num_cores}
RUN make -j${num_cores} check
RUN make install
RUN ldconfig

# ISL 0.21.0
WORKDIR /tmp
ADD isl-0.21.tar.xz ./
WORKDIR /tmp/isl-0.21
RUN ./configure
RUN make -j${num_cores}
RUN make -j${num_cores} check
RUN make install
RUN ldconfig

# GCC 9.2.0
WORKDIR /tmp
ADD gcc-9.2.0.tar.xz ./
WORKDIR /tmp/gcc-9.2.0
RUN ./configure --enable-lto --disable-multilib --enable-languages=c,c++
RUN make -j${num_cores}
RUN make install
RUN ldconfig

FROM debian:10-devtools AS compile-image
MAINTAINER sconstantino@grupobme.es

RUN groupadd postgres && useradd --no-create-home --no-user-group -g postgres postgres
RUN apt-get -y update && apt-get -y install libreadline-dev zlib1g-dev libssl-dev libpam-dev libldap2-dev && rm -rf /var/lib/apt/lists/*
#libpam0g-dev libldap2-dev
#libpam-ldap
WORKDIR /tmp
ADD postgresql-12.0.tar.gz .
WORKDIR /tmp/postgresql-12.0
RUN ./configure --with-pam --with-ldap --with-openssl --with-gnu-ld && make -j$((2*$(nproc --all))) && make install
WORKDIR /tmp
COPY scripts .
RUN chmod 700 pack_installation && ./pack_installation
#RUN make -j$((2*$(nproc --all))) check
#USER postgres
#ENV PATH=/usr/local/pgsql/bin:$PATH
FROM scratch
ADD --chown=postgres:postgres /tmp/rootfs.tar.xz .
USER postgres
ENV PATH=/bin
ENV LD_LIBRARY_PATH=/usr/lib/local/pgsql:/usr/lib/x86_64-linux-gnu:/lib/x86_64-linux-gnu:/lib64
RUN ["id"]
RUN ["tree", "-L", "2"] 
#ENTRYPOINT [""]

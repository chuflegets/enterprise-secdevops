FROM debian:10-devtools
MAINTAINER sconstantino@grupobme.es

#RUN groupadd postgres && useradd --no-create-home --no-user-group -g postgres postgres
#RUN apt-get -y install libreadline-dev zlib1g-dev libssl-dev libpam-dev libldap2-dev
#libpam0g-dev libldap2-dev
#libpam-ldap
WORKDIR /tmp
ADD rt-4.4.4.tar.gz .
WORKDIR /tmp/rt-4.4.4
RUN ./configure --enable-gd --enable-graphviz --enable-developer --enable-externalauth --with-web-handler=fastcgi --with-bin-owner=rt --with-libs-owner=rt --with-libs-group=rt --with-db-type=Pg --with-db-host=pgservice --with-db-port=5432 --with-db-rt-host=localhost --with-db-dba=postgres --with-db-database
RUN make -j$((2*$(nproc --all))) && make install
#RUN make -j$((2*$(nproc --all))) check
#USER postgres
#ENV PATH=/usr/local/pgsql/bin:$PATH
ENTRYPOINT ["/bin/bash"]

FROM debian:10-devtools
MAINTAINER sconstantino@grupobme.es

RUN groupadd postgres && useradd --no-create-home --no-user-group -g postgres postgres
RUN apt-get -y install libreadline-dev zlib1g-dev libssl-dev libpam-dev libldap2-dev
#libpam0g-dev libldap2-dev
#libpam-ldap
WORKDIR /tmp
ADD postgresql-12.0.tar.gz .
WORKDIR /tmp/postgresql-12.0
RUN ./configure --with-pam --with-ldap --with-openssl --with-gnu-ld
RUN make -j$((2*$(nproc --all))) && make install
#RUN make -j$((2*$(nproc --all))) check
#USER postgres
#ENV PATH=/usr/local/pgsql/bin:$PATH
ENTRYPOINT ["/bin/bash"]

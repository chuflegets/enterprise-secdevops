FROM debian:10
MAINTAINER sconstantino@grupobme.es

RUN apt-get -y install libreadline-dev zlib1g-dev libssl-dev libpam0g-dev libldap2-dev libpam-ldap
WORKDIR /tmp
ADD postgresql-12.0.tar.gz .
WORKDIR /tmp/postgresql-12.0
RUN ./configure --with-pam --with-ldap --with-openssl --with-gnu-ld
RUN make -j$((2*$(nproc --all)))
#RUN make -j$((2*$(nproc --all))) check

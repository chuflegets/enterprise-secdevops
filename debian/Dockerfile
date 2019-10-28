FROM debian:10
MAINTAINER sconstantino@grupobme.es

RUN apt-get -y update && apt-get -y upgrade && apt-get -y install build-essential vim tree wget python3 python3-pip
ADD .vimrc /root/.vimrc
ENTRYPOINT ["/bin/bash"]

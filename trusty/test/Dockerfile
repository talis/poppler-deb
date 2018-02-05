FROM ubuntu:trusty

RUN apt-get update

COPY poppler_0.59.0-trusty_amd64.deb /root/

RUN apt-get install -y gdebi
RUN cd /root && gdebi -n poppler_0.59.0-trusty_amd64.deb
RUN /usr/local/bin/convert --version

FROM ubuntu:20.04

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update -y && \
    apt-get upgrade -y && \
    apt-get install -y git nano curl build-essential cmake automake wget && \
    echo "Packages installed"

RUN wget https://downloads.asterisk.org/pub/telephony/asterisk/asterisk-20-current.tar.gz && \
    mv asterisk-20-current.tar.gz /usr/local/src/asterisk-20-current.tar.gz && \
    echo "Asterisk tarball downloaded"

RUN cd /usr/local/src && \
    tar -zxvf asterisk-20-current.tar.gz && \
    echo "Asterisk tarball extracted"

RUN cd /usr/local/src/asterisk-20.4.0/ && \
    ./contrib/scripts/install_prereq install && \
    ./configure && \
    make && \
    make install && \
    make samples && \
    make config && \
    asterisk && \
    echo "Asterisk installed"

COPY "./configs/extensions.conf" /etc/asterisk/extensions.conf
RUN echo "extensions.conf copied"

COPY "./configs/pjsip.conf" /etc/asterisk/pjsip.conf
RUN echo "pjsip.conf copied"

COPY "./configs/http.conf" /etc/asterisk/http2.conf
RUN echo "http.conf copied"

COPY "./configs/manager.conf" /etc/asterisk/manager2.conf
RUN echo "manager.conf copied"

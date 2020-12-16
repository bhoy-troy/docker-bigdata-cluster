FROM ubuntu:20.04

MAINTAINER "James Troy"
ENV DEBIAN_FRONTEND=noninteractive
RUN set -x && \
    apt update -y -qq  && \
    apt install -y --no-install-recommends \
	    build-essential \
        curl \
	    git \
        less \
        nano \
        netcat \
	    net-tools \
        software-properties-common \
        wget \
        python3-dev \
        python3-pip \
        openjdk-8-jdk && \
    apt-get autoclean -y && \
    apt-get autoremove -y && \
    rm -rf /var/lib/apt/lists/*

ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/


# update pip
#RUN apt install python-pip
RUN pip3 install pip wheel --upgrade

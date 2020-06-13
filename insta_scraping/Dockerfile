FROM python:3.7-alpine3.7

RUN pip3 install --upgrade pip
RUN apk update \
  && apk add --virtual build-deps gcc python3-dev musl-dev \
  && apk del build-deps \
  && apk add bash zip


RUN mkdir /aijus-data-sciente-template
ADD . /aijus-data-sciente-template
WORKDIR /aijus-data-sciente-template

RUN python3 setup_aws.py

# Install Oracle Java 8
RUN \
  apt-get update -q -y && \
  apt-get install -y wget unzip software-properties-common && \
  add-apt-repository "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" && \
  apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886 && \
  apt-get update -q && \
  echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
  echo debconf shared/accepted-oracle-license-v1-1 seen true | debconf-set-selections && \
  DEBIAN_FRONTEND=noninteractive apt-get install -y oracle-java8-installer && \
  apt-get clean

RUN pip3 install -r requirements.txt



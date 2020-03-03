FROM ubuntu:18.04

RUN apt update && apt upgrade -y
RUN apt install -y gcc
RUN dpkg --add-architecture i386
RUN apt update
RUN apt install -y libc6:i386 libncurses5:i386 libstdc++6:i386
RUN mkdir /opt/ibm-im
ADD ibm-im /opt/ibm-im
RUN /opt/ibm-im/installc -acceptLicense
RUN rm -rf /opt/ibm-im
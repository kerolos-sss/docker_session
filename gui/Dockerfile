FROM ubuntu:14.04
MAINTAINER Admatic Engineering Team@ADMATIC.IN
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update
# Default jdk
RUN apt-get install --fix-missing -y default-jdk
# 32-bit dependencies of android and utils
RUN apt-get install --fix-missing -y \
    bison \
    git \
    gperf \
    lib32gcc1 \
    lib32bz2-1.0 \
    lib32ncurses5 \
    lib32stdc++6 \
    lib32z1 \
    libc6-i386 \
    libxml2-utils \
    make \
    zip 
# Download and unzip Android Studio for Linux
ADD http://dl.google.com/dl/android/studio/ide-zips/1.2.1.1/android-studio-ide-141.1903250-linux.zip /opt/android-studio.zip
RUN cd /opt/ && unzip android-studio.zip && rm android-studio.zip
CMD /opt/android-studio/bin/studio.sh

# run docker run --net=host --env="DISPLAY" --volume="$HOME/.Xauthority:/root/.Xauthority:rw" android-studio
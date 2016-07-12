FROM debian:8

MAINTAINER Herbert Mühlburger "mail@muehlburger.at"

# Debian 8.0 (Jessie)   # CURRENT TESTING
# RUN echo 'deb http://ftp.de.debian.org/debian/ jessie main contrib non-free' > /etc/apt/sources.list
# deb-src http://ftp.de.debian.org/debian/ jessie main contrib non-free
# deb http://security.debian.org/ jessie/updates main contrib non-free
# deb-src http://security.debian.org/ jessie/updates main contrib non-free
# deb http://ftp.de.debian.org/debian/ jessie-updates main contrib non-free
# deb-src http://ftp.de.debian.org/debian/ jessie-updates main contrib non-free
# deb http://ftp.de.debian.org/debian jessie-backports main contrib non-free
# deb-src http://ftp.de.debian.org/debian jessie-backports main contrib non-free

# Update
RUN apt-get -y update

# Install git
RUN apt-get install -y git aptitude libboost-all-dev swig doxygen

# Make ssh dir
RUN mkdir /root/.ssh/

# Copy over private key, and set permissions
ADD id_rsa /root/.ssh/id_rsa

# Create known_hosts
RUN touch /root/.ssh/known_hosts

# Add github key
RUN ssh-keyscan github.com >> /root/.ssh/known_hosts

# Clone gnucash the repository
RUN git clone https://github.com/muehlburger/gnucash.git

RUN cd gnucash

WORKDIR /gnucash

RUN echo 'deb http://ftp.de.debian.org/debian/ stable main contrib non-free' >> /etc/apt/sources.list
RUN echo 'deb-src http://ftp.de.debian.org/debian/ stable main contrib non-free' >> /etc/apt/sources.list
RUN echo 'deb http://security.debian.org/ stable/updates main contrib non-free' >> /etc/apt/sources.list
RUN echo 'deb-src http://security.debian.org/ stable/updates main contrib non-free' >> /etc/apt/sources.list

RUN apt-get update

RUN apt-get install -y apt-utils autoconf intltool libtool guile-2.0-dev libglib2.0-dev build-essential

RUN apt-get build-dep gnucash

RUN ./autogen.sh

RUN ./configure --prefix=/opt/gnucash-devel --enable-debug --enable-doxygen --enable-error-on-warning --enable-compile-warnings --enable-ofx

#RUN make

#RUN make install

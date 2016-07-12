FROM debian:8

MAINTAINER Herbert Mühlburger "mail@muehlburger.at"

ENV DEBIAN_FRONTEND noninteractive

RUN echo 'deb http://ftp.de.debian.org/debian/ stable main contrib non-free' >> /etc/apt/sources.list
RUN echo 'deb-src http://ftp.de.debian.org/debian/ stable main contrib non-free' >> /etc/apt/sources.list
RUN echo 'deb http://security.debian.org/ stable/updates main contrib non-free' >> /etc/apt/sources.list
RUN echo 'deb-src http://security.debian.org/ stable/updates main contrib non-free' >> /etc/apt/sources.list

# Update
RUN apt-get -y update

# Install git
RUN apt-get install -y \
    git \
    swig \
    doxygen \
    libxml2-dev \
    libxslt1-dev \
    python-dev \
    apt-utils \
    autoconf \
    intltool \
    libtool \
    guile-2.0-dev \
    libglib2.0-dev \
    build-essential \
    xsltproc \
    libui-gxmlcpp-dev \
    libdbi-dev \
    libofx-dev \
    libpython2.7-dev \
    libgnomecanvas2-dev \
    libglib2.0-dev \
    libgtk2.0-dev \
    libgoffice-0.8-dev \
    libboost-dev \
    libdbd-sqlite3 \
    libwebkit-dev
        
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

RUN ./autogen.sh

RUN ./configure --prefix=/opt/gnucash-devel --enable-debug --enable-doxygen --enable-error-on-warning --enable-compile-warnings --enable-ofx

RUN make

RUN make install

from debian:latest

RUN dpkg --add-architecture i386
RUN dpkg --add-architecture amd64

RUN apt-get update && apt-get upgrade && apt-get install -y \
    autoconf \
    automake \
    autopoint \
    bash \
    bison \
    bzip2 \
    flex \
    g++ \
    g++-multilib \
    gettext \
    git \
    gperf \
    intltool \
    libc6-dev-i386 \
    libgdk-pixbuf2.0-dev \
    libltdl-dev \
    libssl-dev \
    libtool-bin \
    libxml-parser-perl \
    lzip \
    make \
    openssl \
    p7zip-full \
    patch \
    perl \
    python \
    ruby \
    sed \
    unzip \
    wget \
    xz-utils
    
RUN git clone https://github.com/mxe/mxe.git
RUN mv mxe /opt/mxe

WORKDIR /opt/mxe
RUN make cc
RUN make pcre libiconv expat libffi glib xz libxml2 zlib  

RUN echo "export PATH=/opt/mxe/usr/bin:$PATH" >> ~/.bashrc

WORKDIR /root
RUN wget https://sourceforge.net/projects/cwb/files/cwb/cwb-3.4-beta/cwb-3.4.22-source.tar.gz
RUN tar xzfv cwb-3.4.22-source.tar.gz
WORKDIR /root/cwb-3.4.22
COPY mxe-cross /root/cwb-3.4.22/config/platform/
RUN sed -i -E "s/^PLATFORM=.*$/PLATFORM=mxe-cross/" /root/cwb-3.4.22/config.mk
RUN sed -i -E "s/^SITE=.*$/SITE=windows-release/" /root/cwb-3.4.22/config.mk
RUN sed -i -E "s/#\s+CC\s*=\s*.*$/CC=i686-w64-mingw32.static-gcc/" /root/cwb-3.4.22/config.mk
RUN sed -i -E "s/#\s+LIBPCRE_DLL_PATH\s+=.*$/LIBPCRE_DLL_PATH = \/opt\/mxe\/usr\/i686-w64-mingw32.static\/lib/" /root/cwb-3.4.22/config.mk
RUN sed -i -E "s/#\s+LIBGLIB_DLL_PATH\s+=.*$/LIBGLIB_DLL_PATH = \/opt\/mxe\/usr\/i686-w64-mingw32.static\/lib/" /root/cwb-3.4.22/config.mk
RUN sed -i -E "s#..MINGW_CROSS_HOME./bin/pcre-config#/opt/mxe/usr/i686-w64-mingw32.static/bin/pcre-config#" definitions.mk

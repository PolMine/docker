# docker run -it --rm -v ~/Lab/github/libcl:/libcl cwbcross:latest

From debian:latest

RUN apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y wget make mingw-w64 unzip xz-utils subversion git pkg-config bison flex

RUN export MINGW_OUTPUT=`x86_64-w64-mingw32-gcc --print-search-dirs | grep ^install | sed -E 's/install:\s(.*?)/\1/'`

# pcre

RUN cd /root && \
  wget https://ftp.pcre.org/pub/pcre/pcre-8.44.tar.gz && \ 
  tar xf pcre-8.44.tar.gz && \
  cd pcre-8.44 && \
  CC=x86_64-w64-mingw32-gcc CC_FOR_BUILD=gcc  ./configure    \
  --host=x86_64-w64-mingw32                                  \
  --enable-utf8 --enable-unicode-properties --enable-jit     \
  --enable-newline-is-any --disable-cpp --enable-static      \
  --disable-dependency-tracking                              \
  --prefix=${MINGW_OUTPUT}                                     \
  --exec-prefix=${MINGW_OUTPUT}                                \
  --libdir=${MINGW_OUTPUT}/lib                                 \
  --oldincludedir=${MINGW_OUTPUT}/include && \
  make && \
  make install


# libiconv

RUN cd /root && \
  wget https://ftp.gnu.org/pub/gnu/libiconv/libiconv-1.16.tar.gz && \
  tar xf libiconv-1.16.tar.gz && \
  cd libiconv-1.16 && \
  CC=x86_64-w64-mingw32-gcc CC_FOR_BUILD=gcc ./configure       \
  --host=x86_64-w64-mingw32                                    \
  --enable-static                                              \
  --prefix=$MINGW_OUTPUT                                       \
  --exec-prefix=$MINGW_OUTPUT                                  \
  --libdir=$MINGW_OUTPUT/lib                                 \
  --oldincludedir=$MINGW_OUTPUT/include && \
  make && \
  make install


# expat

RUN cd /root && \
  wget http://downloads.sourceforge.net/expat/expat-2.4.1.tar.gz && \
  tar xf expat-2.4.1.tar.gz && \
  cd expat-2.4.1 && \
  CC=x86_64-w64-mingw32-gcc CC_FOR_BUILD=gcc ./configure       \
  --host=x86_64-w64-mingw32                                    \
  --prefix=$MINGW_OUTPUT                                       \
  --exec-prefix=$MINGW_OUTPUT                                  \
  --libdir=$MINGW_OUTPUT/lib                                   \
  --oldincludedir=$MINGW_OUTPUT/include && \
  make && \
  make install


### gettext

RUN cd /root && \
  wget https://ftp.gnu.org/gnu/gettext/gettext-0.19.8.tar.gz && \
  tar xf gettext-0.19.8.tar.gz && \
  cd gettext-0.19.8 && \
  CC=x86_64-w64-mingw32-gcc CC_FOR_BUILD=gcc ./configure \
    --enable-static \
    --disable-threads \
    --host=x86_64-w64-mingw32                                    \
    --prefix=${MINGW_OUTPUT}                \
    --exec-prefix=${MINGW_OUTPUT}           \
    --oldincludedir=${MINGW_OUTPUT}/include && \
    make && \
    make install

### libffi

RUN cd /root && \
  wget ftp://sourceware.org/pub/libffi/libffi-3.2.tar.gz && \
  tar xf libffi-3.2.tar.gz && \
  cd libffi-3.2 && \
  LIBFFI_CFLAGS=/usr/lib/gcc/x86_64-w64-mingw32/4.8/include           \
  LIBFFI_LIBS=/usr/lib/gcc/x86_64-w64-mingw32/4.8/lib                   \
  CC=x86_64-w64-mingw32-gcc CC_FOR_BUILD=gcc                            \
  ./configure                                                           \
    --host=x86_64-w64-mingw32                                    \
    --prefix=${MINGW_OUTPUT}                \
    --exec-prefix=${MINGW_OUTPUT}           \
    --oldincludedir=${MINGW_OUTPUT}/include && \
    make && \
    make install

RUN cd /opt && \
  mkdir glib && \
  cd glib && \
  wget  https://download.gnome.org/binaries/win64/glib/2.26/glib-dev_2.26.0-1_win64.zip && \ 
  unzip glib-dev_2.26.0-1_win64.zip && \
  rm glib-dev_2.26.0-1_win64.zip && \
  sed -i -E "s/^prefix=.*$/prefix=\/opt\/glib/" /opt/glib/lib/pkgconfig/glib-2.0.pc

WORKDIR /root
RUN wget https://sourceforge.net/projects/cwb/files/cwb/cwb-3.4-beta/cwb-3.4.22-source.tar.gz
RUN tar xzfv cwb-3.4.22-source.tar.gz
WORKDIR /root/cwb-3.4.22
RUN sed -i -E "s/^PLATFORM=.*$/PLATFORM=mingw-cross/" /root/cwb-3.4.22/config.mk
RUN sed -i -E "s/^SITE=.*$/SITE=windows-release/" /root/cwb-3.4.22/config.mk
RUN sed -i -E "s/#\s+CC\s*=\s*.*$/CC=x86_64-w64-mingw32-gcc/" /root/cwb-3.4.22/config.mk
RUN sed -i -E "s/#\s+LIBPCRE_DLL_PATH\s+=.*$/LIBPCRE_DLL_PATH = \/usr\/lib\/gcc\/x86_64-w64-mingw32\/8.3-win32/" /root/cwb-3.4.22/config.mk
RUN sed -i -E "s/#\s+LIBGLIB_DLL_PATH\s+=.*$/LIBGLIB_DLL_PATH = \/usr\/lib\/gcc\/x86_64-w64-mingw32\/8.3-win32/" /root/cwb-3.4.22/config.mk
# RUN sed -i -E "s#..MINGW_CROSS_HOME./bin/pcre-config#/opt/mxe/usr/i686-w64-mingw32.static/bin/pcre-config#" definitions.mk
RUN sed -i -E "s/i586-mingw32msvc/x86_64-w64-mingw32/g" /root/cwb-3.4.22/config/platform/mingw-cross
RUN sed -i -E "s/i586/x86/" /root/cwb-3.4.22/config/platform/mingw-cross
RUN sed -i -E "s/export\s*PKG_CONFIG_PATH=.+MINGW_CROSS_HOME.\/lib\/pkgconfig\s*;//g" /root/cwb-3.4.22/definitions.mk
RUN sed -i -E "s/\s+\\$\\(MINGW_CROSS_HOME\\)\/bin\/pcre-config/ pcre-config/g" /root/cwb-3.4.22/definitions.mk

RUN sed -i -E "s/^all\\:.*PROGRAMS.$/all: libcqp\\.a/g" /root/cwb-3.4.22/cqp/Makefile
RUN printf '\nlibcqp.a: $(OBJS) $(CQI_OBJS)\n\t$(RM) $@\n\t$(AR) $@ $^\n' >> /root/cwb-3.4.22/cqp/Makefile

ENV PKG_CONFIG_PATH=/opt/glib/lib/pkgconfig  
RUN make clean && make depend && make all


########### COMPILE utils ###############

RUN cd /root && \
  git clone https://github.com/PolMine/RcppCWB.git && \
  cd /root/RcppCWB && \
  git checkout dev && \
  git pull origin dev

WORKDIR /root/RcppCWB/src/cwb/utils

RUN x86_64-w64-mingw32-gcc -c -o _cwb_huffcode.o -O2 -Wall -static  \
  -D__MINGW__ -DEMULATE_SETENV -DG_OS_WIN32                                       \
  -I/root/RcppCWB/src/cwb/cl                                                   \
  -I/usr/share/mingw-w64/include \
  -I$MINGW_OUTPUT/include                                      \
  _cwb_huffcode.c

RUN x86_64-w64-mingw32-gcc -c -o _cwb_compress_rdx.o -O2 -Wall -static  \
  -D__MINGW__ -DEMULATE_SETENV -DG_OS_WIN32                                       \
  -I/root/RcppCWB/src/cwb/cl \
  -I$MINGW_OUTPUT/include                                      \
  _cwb_compress_rdx.c

RUN x86_64-w64-mingw32-gcc -c -o _cwb_encode.o -O2 -Wall -static  \
  -D__MINGW__ -DEMULATE_SETENV -DG_OS_WIN32                                       \
  -I/root/RcppCWB/src/cwb/cl \
  -I$MINGW_OUTPUT/include                                      \
  _cwb_encode.c

RUN x86_64-w64-mingw32-gcc -c -o _cwb_makeall.o -O2 -Wall -static  \
  -D__MINGW__ -DEMULATE_SETENV -DG_OS_WIN32                                       \
  -I/root/RcppCWB/src/cwb/cl                                                   \
  -I/usr/share/mingw-w64/include \
  -I$MINGW_OUTPUT/include                                      \
  _cwb_makeall.c
  
RUN x86_64-w64-mingw32-ar cq libcwb.a _cwb_makeall.o _cwb_huffcode.o _cwb_compress_rdx.o _cwb_encode.o && \
  x86_64-w64-mingw32-ranlib libcwb.a


##### 32 bit ############

RUN export MINGW_OUTPUT_32BIT=`i686-w64-mingw32-gcc --print-search-dirs | grep ^install | sed -E 's/install:\s(.*?)/\1/'`



######### Put crosscompiled files into libcl repo ########

RUN cd /root && \
  git clone https://github.com/PolMine/libcl.git && \
  cd /root/libcl && \
  git checkout dev

RUN cp /root/cwb-3.4.22/cl/libcl.a /root/libcl/lib/x64/libcl.a
RUN cp /root/cwb-3.4.22/cqp/libcqp.a /root/libcl/lib/x64/libcqp.a
RUN cp /root/RcppCWB/src/cwb/utils/libcwb.a /root/libcl/lib/x64/libcwb.a


from fedora:44

RUN yum install -y R

RUN yum install -y gcc-gfortran
ENV CC=clang
ENV CXX=clang++
ENV FC=gfortran
ENV F77=gfortran

# RUN yum install -y glib*
RUN yum install -y pcre2*
RUN yum install -y ncurses
RUN yum install -y bison flex
RUN yum install -y readline* diffutils 
RUN yum install -y xml2* libxml2-devel ssl* protobuf* git
RUN yum install -y --allowerasing --skip-broken curl*
# RUN yum -y install xorg*
RUN yum install -y git
RUN yum install -y sqlite subversion rsync

RUN yum install -y clang clang-devel compiler-rt libomp-devel flang lld

RUN cd ~ && svn co https://svn.r-project.org/R/trunk r-devel/source && mkdir ./r-devel/build

RUN mkdir -p ~/.R && printf 'CC=clang\nCXX=clang++\nCXX11=clang++\nCXX14=clang++\nCXX17=clang++\nCXX20=clang++\nFC=flang-new\nF77=flang-new\n' > ~/.R/Makevars

RUN cd ~/r-devel/source/tools && ./rsync-recommended
RUN cd ~/r-devel/build && ../source/configure --with-x=no && make && make check 
RUN cd /usr/local/bin && ln -s ~/r-devel/build/bin/R R-devel
RUN cd /usr/local/bin && ln -s ~/r-devel/build/bin/Rscript Rscript-devel

RUN Rscript-devel -e 'install.packages(pkgs = c("Rcpp", "knitr", "testthat"), repos = "https://cloud.r-project.org/")'

RUN cd ~ && mkdir git && cd git && git clone https://github.com/PolMine/RcppCWB.git

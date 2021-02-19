from fedora:32

RUN yum install -y R # as of 2020-06-21, this is still R 3.6.3

RUN yum install -y bison flex glib* pcre* ncurses
RUN yum install -y readline* diffutils 
RUN yum install -y xml2* libxml2-devel ssl* protobuf* git
RUN yum install -y --allowerasing --skip-broken curl*
RUN yum -y install xorg*
RUN yum install -y git
RUN yum install -y sqlite subversion rsync

RUN cd ~ && svn co https://svn.r-project.org/R/trunk r-devel/source && mkdir ./r-devel/build
RUN cd ~/r-devel/source/tools && ./rsync-recommended
RUN cd ~/r-devel/build && ../source/configure --with-x=no && make && make check 
RUN cd /usr/local/bin && ln -s ~/r-devel/build/bin/R R-devel
RUN cd /usr/local/bin && ln -s ~/r-devel/build/bin/Rscript Rscript-devel

RUN Rscript-devel -e 'install.packages(pkgs = c("Rcpp", "knitr", "testthat"), repos = "https://cloud.r-project.org/")'

RUN cd ~ && mkdir git && cd git && git clone https://github.com/PolMine/RcppCWB.git
from debian:latest

RUN apt-get update && apt-get install -y gnupg ca-certificates apt-utils software-properties-common dirmngr wget lsb-release

RUN gpg --keyserver keyserver.ubuntu.com --recv-key '95C0FAF38DB3CCAD0C080A7BDC78B2DDEABC47B7'
RUN gpg --armor --export '95C0FAF38DB3CCAD0C080A7BDC78B2DDEABC47B7' | \
    tee /etc/apt/trusted.gpg.d/cran_debian_key.asc
RUN echo "deb http://cloud.r-project.org/bin/linux/debian bookworm-cran40/" >> /etc/apt/sources.list

RUN apt-get update -y && apt-get install -y bison flex libglib2.0-dev libpcre3 libpcre3-dev libncurses5-dev
RUN apt-get update -y && apt-get install -y libcurl4-openssl-dev libssl-dev
RUN apt-get update -y && apt-get install -y libxml2 libxml2-dev
RUN apt-get install -y libprotobuf-dev protobuf-compiler libv8-dev
RUN apt-get install -y texlive-base texinfo texlive-latex-base texlive-latex-extra texlive-fonts-extra texlive-fonts-recommended
RUN apt-get install -y git subversion rsync

# Adapted (slightly) from: https://cran.r-project.org/bin/linux/debian/
# As an alternative, see: http://singmann.org/installing-r-devel-on-linux/

RUN apt-get install -y clang gfortran
RUN apt-get install -y xauth xorg xorg-dev openbox libreadline-dev libbz2-dev liblzma-dev make

RUN cd ~ && svn co https://svn.r-project.org/R/trunk r-devel/source && mkdir ./r-devel/build
RUN cd ~/r-devel/source/tools && ./rsync-recommended
RUN cd ~/r-devel/build && CC="clang-14" CXX="clang++-14" ../source/configure && make && make check 
# RUN make pdf && make info

RUN cd /usr/local/bin && ln -s ~/r-devel/build/bin/R R-devel
RUN cd /usr/local/bin && ln -s ~/r-devel/build/bin/Rscript Rscript-devel

# Note that the only entry on .libPaths() is $RTOP/r-devel/build/library, 
# so this is where packages will be installed.

RUN Rscript-devel -e 'install.packages("polmineR", repos = "https://cran.uni-muenster.de/")'

RUN Rscript-devel -e 'install.packages( \
  pkgs = c( \
    "markdown", "rmarkdown", "htmltools", "openxlsx", "sendmailR", "shiny", \
    "shinythemes", "miniUI", "rhandsontable", "testthat", "tidytext", "covr", \
    "igraph", "NLP", "httr", "curl", "highlight", "shinyjs", "webshot", \
    "protolite", "V8"\
    ), \
    repos = "https://cran.uni-muenster.de/" \
  )'

RUN cd ~ && mkdir git && cd git && git clone https://github.com/PolMine/polmineR.git

RUN apt-get update && apt-get install -y locales

RUN echo "LC_ALL=en_US.UTF-8" >> /etc/environment
RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen
RUN echo "LANG=en_US.UTF-8" > /etc/locale.conf
RUN locale-gen en_US.UTF-8

RUN apt-get install -y pandoc
RUN apt-get install -y tidy

RUN ln -s /usr/lib/R/library/grDevices/libs/cairo.so /root/r-devel/build/library/grDevices/libs/cairo.so

RUN echo "export LC_ALL=en_US.UTF-8" >> ~/.bashrc && . ~/.bashrc

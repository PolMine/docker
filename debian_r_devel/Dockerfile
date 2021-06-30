from debian:latest

# Install R from mirror. Why? We build R-devel later on, but this may ensure presence of dependencies

RUN apt-get update && apt-get install -y gnupg ca-certificates apt-utils
RUN apt-get update && apt-get install -y r-base r-base-dev


# Install dependencies (for R packages installed later on)

RUN apt-get update -y && apt-get install -y bison flex libglib2.0-dev libpcre3 libpcre3-dev libncurses5-dev
RUN apt-get update -y && apt-get install -y libcurl4-openssl-dev libssl-dev
RUN apt-get update -y && apt-get install -y libxml2 libxml2-dev
RUN apt-get install -y libprotobuf-dev protobuf-compiler libpcre2-dev pcre2-utils
RUN apt-get install -y libsodium-dev openjdk-11-jdk default-jre


# Install tex

RUN apt-get install -y texlive-base texinfo texlive-latex-base texlive-latex-extra texlive-fonts-extra texlive-fonts-recommended

# Install sync tools

RUN apt-get install -y git subversion rsync

# Adapted (slightly) from: https://cran.r-project.org/bin/linux/debian/
# As an alternative, see: http://singmann.org/installing-r-devel-on-linux/

RUN apt-get install -y -q dialog
RUN apt-get install -y xauth openbox
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y xorg xorg-dev # use envvar to suppress user dialogue for keyboard-configuration


RUN cd ~ && svn co https://svn.r-project.org/R/trunk r-devel/source && mkdir ./r-devel/build
RUN cd ~/r-devel/source/tools && ./rsync-recommended
RUN cd ~/r-devel/build && ../source/configure && make && make check

# We do not run make pdf, because latex is not installed
# RUN make pdf && make info

RUN cd /usr/local/bin && ln -s ~/r-devel/build/bin/R R-devel
RUN cd /usr/local/bin && ln -s ~/r-devel/build/bin/Rscript Rscript-devel

# Note that the only entry on .libPaths() is $RTOP/r-devel/build/library,
# so this is where packages will be installed.

RUN Rscript-devel -e 'install.packages("polmineR", repos = "https://cran.rstudio.com/")'

RUN Rscript-devel -e 'install.packages(pkgs = c("markdown", "rmarkdown", "htmltools", "openxlsx", "sendmailR", "shiny", "shinythemes", "miniUI", "rhandsontable", "testthat", "tidytext", "covr", "igraph", "NLP", "httr", "curl", "zen4R", "openNLP", "aws.s3", "rJava", "knitr"), repos = "https://cran.uni-muenster.de/")'
RUN Rscript-devel -e 'install.packages("webshot", repos = "https://cran.uni-muenster.de/")'
RUN Rscript-devel -e 'install.packages("protolite", repos = "https://cran.uni-muenster.de/")'
RUN R-devel CMD javareconf

RUN cd ~ && mkdir git && cd git && git clone https://github.com/PolMine/polmineR.git

RUN apt-get update && apt-get install -y locales

RUN echo "LC_ALL=en_US.UTF-8" >> /etc/environment
RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen
RUN echo "LANG=en_US.UTF-8" > /etc/locale.conf
RUN locale-gen en_US.UTF-8

RUN apt-get install -y pandoc pandoc-citeproc

RUN ln -s /usr/lib/R/library/grDevices/libs/cairo.so /root/r-devel/build/library/grDevices/libs/cairo.so

RUN apt-get -y install locales
RUN locale-gen en_US.UTF-8
RUN update-locale LANG=en_US.UTF-8
RUN echo "LANG=en_US.UTF-8" >> ~/.Renviron


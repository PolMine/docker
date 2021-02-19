from debian:latest

RUN apt-get update && apt-get install -y gnupg ca-certificates apt-utils
RUN echo "deb https://cran.uni-muenster.de/bin/linux/debian buster-cran35/" >> /etc/apt/sources.list
RUN apt-key adv --keyserver keys.gnupg.net --recv-key 'E19F5F87128899B192B1A2C2AD5F960A256A04AF' && \
  apt-get update && \
  apt-get install -y r-base r-base-dev

RUN apt-get update -y && apt-get install -y bison flex libglib2.0-dev libpcre3 libpcre3-dev libncurses5-dev
RUN apt-get update -y && apt-get install -y libcurl4-openssl-dev libssl-dev
RUN apt-get update -y && apt-get install -y libxml2 libxml2-dev
RUN apt-get install -y libprotobuf-dev protobuf-compiler

RUN apt-get install -y texlive-base texinfo texlive-latex-base texlive-latex-extra texlive-fonts-extra texlive-fonts-recommended

# RUN Rscript -e 'install.packages("polmineR")'
# RUN Rscript -e 'install.packages("devtools")'

RUN apt-get install -y git

RUN apt-get install -y subversion
RUN apt-get install -y rsync

# Adapted (slightly) from: https://cran.r-project.org/bin/linux/debian/
# As an alternative, see: http://singmann.org/installing-r-devel-on-linux/

RUN apt-get install -y -q dialog
RUN apt-get install -y xauth 
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y xorg
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y xorg-dev # use envvar to suppress user dialogue for keyboard-configuration
RUN apt-get install -y openbox

RUN cd ~ && svn co https://svn.r-project.org/R/trunk r-devel/source && mkdir ./r-devel/build
RUN cd ~/r-devel/source/tools && ./rsync-recommended
RUN cd ~/r-devel/build && ../source/configure && make && make check 
# We do not run make pdf, because latex is not installed 
# RUN make pdf && make info

RUN cd /usr/local/bin && ln -s ~/r-devel/build/bin/R R-devel
RUN cd /usr/local/bin && ln -s ~/r-devel/build/bin/Rscript Rscript-devel

# Note that the only entry on .libPaths() is $RTOP/r-devel/build/library, 
# so this is where packages will be installed.

RUN Rscript-devel -e 'install.packages("polmineR", repos = c("https://cran.rstudio.com/", "https://polmine.github.io/drat/"))'

RUN Rscript-devel -e 'install.packages(pkgs = c("markdown", "rmarkdown", "htmltools", "openxlsx", "sendmailR", "shiny", "shinythemes", "miniUI", "rhandsontable", "testthat", "tidytext", "covr", "igraph", "NLP", "httr", "curl"), repos = "https://cran.uni-muenster.de/")'
RUN Rscript-devel -e 'install.packages("webshot", repos = "https://cran.uni-muenster.de/")'
RUN Rscript-devel -e 'install.packages("protolite", repos = "https://cran.uni-muenster.de/")'

RUN cd ~ && mkdir git && cd git && git clone https://github.com/PolMine/polmineR.git

RUN apt-get update && apt-get install -y locales

RUN echo "LC_ALL=en_US.UTF-8" >> /etc/environment
RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen
RUN echo "LANG=en_US.UTF-8" > /etc/locale.conf
RUN locale-gen en_US.UTF-8

RUN apt-get install -y pandoc pandoc-citeproc

RUN ln -s /usr/lib/R/library/grDevices/libs/cairo.so /root/r-devel/build/library/grDevices/libs/cairo.so

# RUN echo "export LC_ALL=en_US.UTF-8" >> ~/.bashrc && source ~/.bashrc

from debian:latest

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
  gnupg \
  ca-certificates \
  apt-utils

RUN echo "deb https://cran.uni-muenster.de/bin/linux/debian buster-cran35/" >> /etc/apt/sources.list && \
  apt-key adv --keyserver keys.gnupg.net --recv-key 'E19F5F87128899B192B1A2C2AD5F960A256A04AF' && \
  apt-get update && \
  apt-get install -y \
  r-base \
  r-base-dev

RUN apt-get update -y && apt-get install -y \
  bison \
  flex \
  libglib2.0-dev \
  libpcre3 \
  libpcre3-dev \
  libncurses5-dev

RUN apt-get update -y && apt-get install -y \
  libcurl4-openssl-dev \
  libssl-dev \
  libxml2 \
  libxml2-dev \
  libgsl-dev

RUN apt-get install -y \
  libprotobuf-dev \
  protobuf-compiler

RUN apt-get install -y texlive-base texinfo \
  texlive-latex-base \
  texlive-latex-extra \
  texlive-fonts-extra \
  texlive-fonts-recommended

RUN Rscript -e 'install.packages("polmineR")'
RUN Rscript -e 'install.packages(pkgs = c("markdown", "rmarkdown", "htmltools", "openxlsx", "sendmailR", "shiny", "shinythemes", "miniUI", "rhandsontable", "testthat", "tidytext", "covr", "igraph", "NLP", "httr", "curl"), repos = "https://cran.uni-muenster.de/")'

RUN Rscript -e 'install.packages("devtools")'

RUN apt-get install -y git
RUN cd ~ && mkdir git && cd git && git clone https://github.com/PolMine/polmineR.git

RUN apt-get update && apt-get install -y locales

RUN echo "LC_ALL=en_US.UTF-8" >> /etc/environment
RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen
RUN echo "LANG=en_US.UTF-8" > /etc/locale.conf
RUN locale-gen en_US.UTF-8
RUN echo "export LC_ALL=en_US.UTF-8" >> ~/.bashrc && /bin/bash -c "source ~/.bashrc"

# RUN ln -s /usr/lib/R/library/grDevices/libs/cairo.so /root/r-devel/build/library/grDevices/libs/cairo.so


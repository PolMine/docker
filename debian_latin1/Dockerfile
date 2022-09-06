from debian:latest

RUN apt-get update && apt-get install -y gnupg ca-certificates apt-utils


RUN apt-get install -y locales && \
  echo "de_DE ISO-8859-1" >> /etc/locale.gen && \
  locale-gen && \
  echo "export LC_ALL=de_DE.iso88591" >> ~/.bashrc && \
  echo "export LANG=de_DE.iso88591" >> ~/.bashrc && \
  echo "export LANGUAGE=de_DE.iso88591" >> ~/.bashrc

RUN apt-get install -y r-base r-base-dev

RUN apt-get update -y && apt-get install -y bison flex libglib2.0-dev libpcre3 libpcre3-dev libncurses5-dev
RUN apt-get update -y && apt-get install -y libcurl4-openssl-dev libssl-dev
RUN apt-get update -y && apt-get install -y libxml2 libxml2-dev
RUN apt-get install -y libprotobuf-dev protobuf-compiler

RUN Rscript -e 'install.packages(pkgs = c("polmineR", "devtools", "markdown", "rmarkdown", "htmltools", "openxlsx", "sendmailR", "shiny", "shinythemes", "miniUI", "rhandsontable", "testthat", "tidytext", "covr", "igraph", "NLP", "httr", "curl", "webshot", "protolite"), repos = "https://cran.uni-muenster.de/")'

RUN apt-get install -y git
RUN cd ~ && mkdir git && cd git && git clone https://github.com/PolMine/polmineR.git

RUN mkdir /opt/cwb && \
  mkdir /opt/cwb/registry && \
  mkdir /opt/cwb/registry_tmp && \
  mkdir /opt/cwb/indexed_corpora 

ENV CORPUS_REGISTRY=/opt/cwb/registry
RUN echo "CORPUS_REGISTRY=/opt/cwb/registry" > ~/.Renviron

ENTRYPOINT cp /opt/cwb/registry_tmp/* /opt/cwb/registry/ && \ 
  for file in $(ls /opt/cwb/registry); do sed -i -r 's#^HOME\s.*/(.*?)#HOME /opt/cwb/indexed_corpora/\1#g' /opt/cwb/registry/$file; done && \
  /bin/bash

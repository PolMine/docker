FROM opencpu/ubuntu-18.04

RUN apt-get update && apt-get install -y --no-install-recommends apt-utils dialog

RUN apt-get update -y && apt-get install -y bison \
  flex \
  libglib2.0-dev \
  libpcre3 \
  libpcre3-dev \
  libncurses5-dev \
  libncursesw5-dev \ 
  libcurl4-openssl-dev \
  libssl-dev

RUN Rscript -e 'install.packages(pkgs = c("polmineR", "remotes"), repos = "https://cran.rstudio.com/")'
RUN Rscript -e 'remotes::install_github("PolMine/polmineR", ref = "dev")'

RUN mkdir /opt/data && \
  mkdir /opt/data/cwb && \
  mkdir mkdir /opt/data/cwb/registry && \
  mkdir /opt/data/cwb/indexed_corpora
  
ENV CORPUS_REGISTRY=/opt/data/cwb/registry

RUN sed -i 's/"preload":\s\["lattice"\]/"preload": ["polmineR"]/' /etc/opencpu/server.conf
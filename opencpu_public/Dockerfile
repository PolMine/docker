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
RUN Rscript -e 'remotes::install_github("PolMine/polmineR", ref = "dev", build_vignettes = FALSE)'

RUN mkdir /opt/data && \
  mkdir /opt/data/cwb && \
  mkdir mkdir /opt/data/cwb/registry && \
  mkdir /opt/data/cwb/indexed_corpora
  
ENV CORPUS_REGISTRY=/opt/data/cwb/registry

RUN Rscript -e 'install.packages(pkgs = "cwbtools", repos = "https://cran.rstudio.com/")'
RUN Rscript -e 'remotes::install_github("PolMine/cwbtools", ref = "dev", build_vignettes = FALSE)'

RUN Rscript -e 'cwbtools::corpus_install(doi = "https://doi.org/10.5281/zenodo.3823245")'

RUN sed -i 's/"preload":\s\["lattice"\]/"preload": ["polmineR"]/' /etc/opencpu/server.conf

ENV POLMINER_USE_TMP_REGISTRY=false
RUN touch ~/.Renviron && echo "POLMINER_USE_TMP_REGISTRY=false" >> ~/.Renviron
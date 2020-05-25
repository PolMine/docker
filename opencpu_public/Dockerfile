FROM opencpu/ubuntu-20.04

RUN apt-get update && apt-get install -y --no-install-recommends apt-utils dialog bison flex  libglib2.0-dev libpcre3 libpcre3-dev libncurses5-dev libncursesw5-dev libcurl4-openssl-dev libssl-dev && \
    rm -rf /var/lib/apt/lists/* && apt clean

RUN  mkdir -p /opt/data/cwb/registry /opt/data/cwb/indexed_corpora
  
ENV CORPUS_REGISTRY=/opt/data/cwb/registry


RUN Rscript -e 'install.packages(pkgs = c("polmineR", "remotes"), repos = "https://cran.rstudio.com/")'  && \
    Rscript -e 'remotes::install_github("PolMine/polmineR", ref = "dev", build_vignettes = FALSE)' && \
    Rscript -e 'install.packages(pkgs = "cwbtools", repos = "https://cran.rstudio.com/")' && \
    Rscript -e 'remotes::install_github("PolMine/cwbtools", ref = "dev", build_vignettes = FALSE)' && \
    Rscript -e 'cwbtools::corpus_install(doi = "https://doi.org/10.5281/zenodo.3823245")' && \
    rm -rf /tmp/downloaded_packages/ /tmp/*.rds

RUN sed -i 's/"preload":\s\["lattice"\]/"preload": ["polmineR"]/' /etc/opencpu/server.conf

ENV POLMINER_USE_TMP_REGISTRY=false
RUN touch ~/.Renviron && echo "POLMINER_USE_TMP_REGISTRY=false" >> ~/.Renviron
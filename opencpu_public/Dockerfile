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

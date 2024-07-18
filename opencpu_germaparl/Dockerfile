FROM polmine/opencpu_public

# RUN Rscript -e 'remotes::install_github("PolMine/cwbtools", ref = "dev")'
# RUN Rscript -e 'remotes::install_github("PolMine/GermaParl", ref = "dev")'
# RUN Rscript -e 'GermaParl::germaparl_download_corpus()'

RUN Rscript -e 'cwbtools::corpus_install(doi = "https://doi.org/10.5281/zenodo.10416536")'

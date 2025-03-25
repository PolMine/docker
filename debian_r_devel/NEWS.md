[2025-03-25]
  - update from opendjdk 11 to openjdk 17
  - pandoc-citeproc temporarily commented out (deprecated or not yet available for Debian bookworm)

[2021-06-25] 
  - setting locale adapted from bignlp docker file
  - no key for R mirror
  - pcre2 installed because it is required by R-devel

[2021-06-05] R packages installed for checking cwbtools: 
  - additional R packages installed: zen4R, openNLP, aws.s3, rJava", knitr
  - apt-get install -y libsodium-dev openjdk-11-jdk default-jre 
  - R-devel CMD javareconf
  - setting locale at end not commented out any more

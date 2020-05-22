## About the docker image 'opencpu_public'

The image starts from opencpu/ubuntu-18.04, which includes an installation of R and of OpenCPU server. The Dockerfile installs system requirements for the Corpus Worbench included in the RcppCWB package. Finally, the latest development version of polmineR is installed, using the mechanism to install package from GitHub offered by the remotes package.

```sh
docker pull polmine/opencpu_public:latest # 
docker run -i -t opencpu_public:latest /bin/bash # start interactive mode, for testing purposes
docker run -t -p 8004:8004 opencpu_public:latest # run on localhost
curl http://localhost:8004/ocpu/info # check that opencpu is available and running
```

This is a check you can run locally.

```r
library(polmineR)
x <- corpus("REUTERS", server = "http://localhost:8004")
y <- size(x)
show(y)
```

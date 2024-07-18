## About the docker image 'opencpu_public'

The image starts from opencpu/ubuntu-22.04, which includes an installation of R and of OpenCPU server. For Apple Silicon machines, the image is not available at Docker Hub and needs to be build locally. The Dockerfile is available here: https://github.com/opencpu/opencpu-server

The Dockerfile installs system requirements for the Corpus Worbench included in the RcppCWB package. Finally, the latest development versions of polmineR and cwbtools are installed.

```sh
cd ~/Lab/github/docker/opencpu_public
docker build -t ocpu_public:latest .
docker pull polmine/opencpu_public:latest # not updated
docker run -i -t opencpu_public:latest /bin/bash # start interactive mode, for testing purposes
docker run -t -p 8004:8004 opencpu_public:latest # run on localhost
docker run -t -p -d 8004:8004 opencpu_public:latest # run on localhost, demon mode
curl http://localhost:8004/ocpu/info # check that opencpu is available and running
```

This is a check you can run locally.

```r
library(polmineR)
x <- corpus("GERMAPARLSAMPLE", server = "http://localhost:8004", restricted = FALSE)
y <- size(x)
show(y)
```


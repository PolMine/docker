## About the docker image 'opencpu_restricted'

The image starts from the image 'polmine/opencpu_public', which adds an installation of polmineR to the installation of R and of OpenCPU Server offered by the image 'opencpu/ubuntu-18.04'. 

The Dockerfile for 'opencpu_restricted' is intended to serve as a demo, and the intended usage of the image is local testing purposes. Quite obviously, a serious use case requires the installation of furthere corpus data, and sufficiently strong passwords for real users. A real world-example for using the 'polmine/opencpu_public' image is to host a corpus with licensed data on a server (e.g. amazon EC2).

```sh
docker pull polmine/opencpu_restricted:latest # 
docker run -i -t opencpu_restricted:latest /bin/bash # start interactive mode, for testing purposes
docker run -t -p 8004:8004 opencpu_restricted:latest # run on localhost
curl http://localhost:8004/ocpu/info # check that opencpu is available and running
```

This is a check you can run locally.

```r
library(polmineR)
x <- corpus("REUTERS", server = "http://localhost:8004", user = "demo", password = "demopass")
y <- size(x)
show(y)
```

The purpose of this Dockerfile is to offer an environment for testing and
debugging polmineR functionality in an R session with a latin1 charset. This may
be useful for dealing with bugs encountered on Windows, but when no Windows
machine with sufficient resources is available.

Build the docker image as usual, e.g. by running the following command in this
directory with the Dockerfile.

```sh
docker build -t polmine/debian-latin1:latest .
```

The Dockerfile is based on the assumption that you want to access corpora 
available on your host from your container. Map the path to the corpus registry
and the superdirectory of the home directory when starting the container

```sh
docker run -it --rm \
  -v ~/Data/cwb/indexed_corpora:/opt/cwb/indexed_corpora \
  -v ~/Data/cwb/registry:/opt/cwb/registry_tmp \
  polmine/debian-latin1:latest \
  /bin/bash
```

Upon starting the container, the HOME directories in the registry files will 
be modified to refer to the locations within the container. 

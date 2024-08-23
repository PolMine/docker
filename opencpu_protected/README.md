## About the docker image 'opencpu_protected'

### Building the container 

### Testing the container

### Server install

```sh
docker run -t -d \
    -v /usr/local/apache2/htdocs:/usr/local/apache2/htdocs \
    -v /opt/data/cwb/registry:/opt/data/cwb/registry \
    -v /opt/data/cwb/indexed_corpora:/opt/data/cwb/indexed_corpora \
    -p 8004:8004 \
    ocpu_public:latest
```

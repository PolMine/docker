FROM polmine/opencpu_public

ARG AWS_ACCESS_KEY_ID
ARG AWS_SECRET_ACCESS_KEY

RUN mkdir /root/tmp
WORKDIR /root/tmp

RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && \
  unzip awscliv2.zip && \ 
  sudo ./aws/install

RUN mkdir ~/.aws && \
  touch ~/.aws/credentials && \
  echo "[default]" >> ~/.aws/credentials && \
  echo "aws_access_key_id = ${AWS_ACCESS_KEY_ID}" >> ~/.aws/credentials && \
  echo "aws_secret_access_key = ${AWS_SECRET_ACCESS_KEY}" >> ~/.aws/credentials && \
  touch ~/.aws/config && \
  echo "[default]" >> ~/.aws/config && \ 
  echo "output = json" >> ~/.aws/config && \ 
  echo "region = eu-central-1" >> ~/.aws/config

RUN aws s3 cp s3://polmine/corpora/cwb/germaparl/germaparl.tar.gz .

RUN Rscript -e 'remotes::install_github("PolMine/cwbtools", ref = "dev")'

RUN Rscript -e 'cwbtools::corpus_install(tarball = "germaparl.tar.gz", registry_dir = "/opt/data/cwb/registry")'

RUN rm -r /root/tmp

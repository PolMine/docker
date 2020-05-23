```sh
docker build \
  --build-arg AWS_ACCESS_KEY_ID=$(grep "aws_access_key_id" ~/.aws/credentials | awk '{print $3}') \
  --build-arg AWS_SECRET_ACCESS_KEY=$(grep "aws_secret_access_key" ~/.aws/credentials | awk '{print $3}') \
  --tag opencpu_restricted_migpress:v0.0.1 \
  opencpu_restricted_migpress
```

Irgendwann reicht EBS-Speicher nicht. Anleitung zum Speicher vergrößern:
https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/recognize-expanded-volume-linux.html


```sh
sudo yum update -y
sudo amazon-linux-extras install docker
sudo service docker start
sudo usermod -a -G docker ec2-user

# log out and log in to make changes effective
docker info

sudo yum -y install git

cd ~
mkdir git
cd git

ssh-keygen -t rsa -b 2048 -C "andreas.blaette@uni-due.de"

cat /home/ec2-user/.ssh/id_rsa.pub
# gitlab hinterlegen

git clone git@gitlab.sowi.uni-due.de:polmine/migpressdocker.git

mkdir ~/.aws
nano ~/.aws/credentials # credentials einfügen

cd migpressdocker
```

Dann Aufruf Befehl oben.


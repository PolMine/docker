## Using the opencpu_germaparl image

This is a short walkthrough how to host the opencpu_germaparl image on an amazon EC2 instance.

At first, update packages on the fresh machine.

```sh
sudo yum update -y
```

Then, install and start docker, and change user rights to omit having to use sudo rights.

```sh
sudo amazon-linux-extras install docker
sudo service docker start
sudo usermod -a -G docker ec2-user
```

You need to log out and to log in again to make changes effective. Check whether everything works as follows.

```sh
docker info
```

Now pull the docker image ... 

```sh
docker pull polmine/opencpu_germaparl
```

... and start it and put it on port 80.

```sh
docker run -d -p 80:80 opencpu_germaparl:latest 
```

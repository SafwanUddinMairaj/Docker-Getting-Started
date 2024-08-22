## INSTALL DOCKER

A very detailed instructions to install Docker are provide in the below link

https://docs.docker.com/get-docker/

For Demo, 

create an Ubuntu EC2 Instance on AWS and run the below commands to install docker.

```
sudo apt update
sudo apt install docker.io -y
```


### Start Docker and Grant Access

Ensure the docker daemon is up and running.

A easy way to verify Docker installation is by running the below command

```
docker run hello-world
```

If the output:

```
docker: Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Post "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/create": dial unix /var/run/docker.sock: connect: permission denied.
See 'docker run --help'.
```

This can mean two things, 
1. Docker deamon is not running.
2. user does not have access to run docker commands.


### Start Docker daemon

Use the below command to verify if the docker daemon is actually started and Active

```
sudo systemctl status docker
```

If you notice that the docker daemon is not running, start the daemon using the below command

```
sudo systemctl start docker
```


### Grant Access to your user to run docker commands

To grant access to the user to run the docker command, you should add the user to the Docker Linux group. Docker group is created by default when docker is installed.

```
sudo usermod -aG docker ubuntu
```

In the above command `ubuntu` is the name of the user, you can change the username appropriately.

**NOTE:** : After doing the above process, Logout and login back for the changes to be reflected.


### Docker is Installed, up and running!

Use the same command again, to verify that docker is up and running.

```
docker run hello-world
```

Output should look like:

```
....
....
Hello from Docker!
This message shows that your installation appears to be working correctly.
...
...
```


## You can start with this repository to write your first Dockerfile.

### Clone this repository:

```
git clone https://github.com/SafwanUddinMairaj/Docker-Getting-Started.git

```

### Login to Docker [Create an account with https://hub.docker.com/]

```
docker login
```

```
Login with your Docker ID to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com to create one.
Username: [your-username]
Password: [your-password]
WARNING! Your password will be stored unencrypted in /home/ubuntu/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
```

### Build your first Docker Image

Change the username accoringly in the below command

```
docker build -t [your-username]/first-docker-image:latest .
```

Output of the above command

```
    Sending build context to Docker daemon     64kB
Step 1/6 : FROM ubuntu:latest
 ---> edbfe74c41f8
Step 2/6 : WORKDIR /app
 ---> Using cache
 ---> 057588ee13a5
Step 3/6 : COPY . /app
 ---> Using cache
 ---> 670dc1e9ea6b
Step 4/6 : RUN apt-get update && apt-get install -y python3 python3-pip
 ---> Using cache
 ---> 97cf4b7c64c8
Step 5/6 : ENV NAME World
 ---> Using cache
 ---> 41124e768175
Step 6/6 : CMD ["python3", "app.py"]
 ---> Using cache
 ---> b95a7687c066
Successfully built b95a7687c066
Successfully tagged [your-username]/first-docker-image:latest


```

### Verify Docker Image is created

```
docker images
```

Output 

```
REPOSITORY                        TAG       IMAGE ID       CREATED          SIZE
your-username/first-docker-image  latest    b95a7687c066   21 minutes ago   573MB
ubuntu                            latest    edbfe74c41f8   3 weeks ago      78.1MB
hello-world                       latest    d2c94e258dcb   15 months ago    13.3kB

```

### Run your First Docker Container

```
docker run -it [your-username]/my-first-docker-image
```

Output

```
Hello World
```

### Push the Image to DockerHub and share it with the world

```
docker push [your-username]/first-docker-image
```

Output

```
Using default tag: latest
The push refers to repository [docker.io/your-username/first-docker-image]
4395a4727380: Pushed
48c1988c5c93: Pushed
85463bd6b633: Pushed
f36fd4bb7334: Mounted from library/ubuntu
latest: digest: sha256:a779ba5a9320c157e6ad7784c09ad9b15392346f69a5822a68b16cf73e78119c size: 1157

```
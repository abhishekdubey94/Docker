
# DOCKER
## Why Docker?
Docker makes it really easy to install and run software without worrying about setup or dependencies.

An image is a single file containing all the dependencies and all the configuration required to run a very specific program. We can use this image to create something called a container.
A container is an instance of an image (a running program).It is a program with its own isolated set of hardware resources.

## Docker Commands

- run - to run the image, if the image is not present it will download from the docker hub.
- run -d option - runs in background (detached mode)
- run -i option - interactive mode (for input)
- run -t option - terminal mode (for prompt)
- run *command* - to run the command in the container, the command should be a valid program for the container file system. 
**note** : This command gets stored as default for the container and if you start the same container again with the id, it will not take up the command again
**note** if the command is **sh**, it will open up a shell to interact with container.
- attach - to attach back to the background container.
- ps - it lists all the container running on the docker
- ps --all - it lists all the containers that we ever created
- create &lt;image name> - creates the image
- start &lt;image name or id> - start the image, -a will attach and show the output
- stop - to stop the container, give id or name of the container to stop (gives some time to process to cleanup)
- kill - to kill the container immediately
- rm - to remove the container
- images - to list the images
- rmi - to remove the image (make sure no container of this image is running)
- pull - to download the image and not run.
- exec - to execute a command on a running container e.g docker exec &lt;running container name or id> &lt;command to exec>
- exec -it &lt;container id or name&gt; **sh** - to attach shell to the container to run commands in the container
- system prune - deletes all the images and stopped containers

Containers are not made to run os. If you run ubuntu, it wil run and exit immediately. This is because, containers are made to run a specific process or task and not the os. If the task gets completed, it exits.

Port mapping : To access an application inside docker container. There are two ways
1. To use the ip address of the docker container, every docker has an ip address associated with it. The port number is same as the port number of the application inside the docker. It is an internal ip which can be used inside the docker host only.
2. Another way is to use the ip address of the host along with mapping the port number of the application with some other port number. This can be acheived using **-p newport : port** option with run.
e.g. docker run -p &lt;outside port&gt; : &lt;inside port&gt; &lt;imageid&gt;
**Note** : There is no restriction for docker container to access network outside container.
3. Docker container has its own file system. To persist the data outside the container, map the directory outside the container. This can be achieved using **-v *outside container dir : inside container dir*** option with run command.
4. To get details of the container, use **inspect** command.
5. To view the logs of the container(stopped or running), use **logs** command.
6. To set the environment variable in the container pass it with **-e key=value**. e.g *docker run -e APP_COLOR=blue ImageName*
7. To check the environment variable, run the inspect command. e.g *docker inspect containerName*
8. To change working directory of dockerfile, use **WORKDIR** <file system inside container> e.g. WORKDIR /usr/app <br/>
Any command following will be with respect to this workinf directory. like COPY

## To Create Docker Image With Dockerfile
1. Create a Dockerfile having all the steps of deployment of the application.
    - Specify a base image.
    - Run some commands to install additional programs
    - Specify a command to run on container startup
2. Then build the docker image using docker build command and specifying the dockerfile, name and tag of the image e.g *docker build Dockerfile -t myapp*
3. To publish on dockerhub use **push** . e.g. *docker push myapp*
4. Dockerfile is in Instruction and Argument format. 
5. Dockerfile should start with base OS or another image which contains it always. e.g FROM Ubuntu
6. To run a command use RUN. e.g. RUN apt-get update
7. When dockered builds images, it builds in layered manner.
8. *docker history imageName*
9. In dockerfile we have **CMD** which defines what will be started when the container starts for that image. In case of Ubuntu image's dockerfile, we have CMD ["bash"]. The bash command looks for terminal, if it doesn't find it exits. To run such container, we need to add a command like *docker run ubuntu sleep 5*.
10. To specify command in CMD in dockerfile, use shell command like CMD sleep 5 or use json array format like CMD ["sleep","5"]
11. To send the arg from docker run command, the dockerfile should have the **ENTRYPOINT**. It appends the argument which we pass by running command. e.g. ENTRYPOINT ["sleep"].
12. To have a default value in the argument, we specify CMD after ENTRYPOINT.
13. We can also specify --entrypoint in docker run command. e.g. docker run --entrypoint sleep2.0 ubuntu 10
14. To have necessary build files during image creation with dockerfile, we can use COPY command . COPY &lt;relative local directory&gt; &lt;File system on image&gt;
15. To change working directory of dockerfile, use **WORKDIR** <file system inside container> e.g. WORKDIR /usr/app <br/>
Any command following will be with respect to this working directory. like COPY
16. To specify the docker file explicitly, use **-f** option.
e.g. docker build -f &lt;docker file name&gt; &lt;resource directory&gt;

### To Create Docker Image With Running Container
- commit - It will create an image from an existing running container
e.g. docker commit -c 'CMD ["redis-server"]' &lt;Name or id of container&gt;

## Docker-Compose
1. It is a separate cli tool, that gets installed with the docker.
2. Can be used to start up multiple Docker containers at the same time.
3. Automates some of the long-winded arguments we were passing to 'docker run'
4. In docker compose, the services (i.e. container) have access to each other networks without opening up the ports. Ports have to be opne only to access from localhost.
5. **docker-compose up** is similar to **docker run myimage**
6. **docker-compose up --build** is similar to **docker build .** + **docker run myimage**
7. docker-compose creates a network which joins different container.
8. In the app, wherever we want to have a connection like http://, we can use the service name from the services part of docker-compose.
9. **docker-compose up -d** To start all the containers in background use.
10. **docker-compose down** to stop all the containers.
11. Restart policies - "no"(default) in quotes, always,on-failure, unless-stopped
12. **docker-compose ps** - shows running containers . **IMPORTANT** it should be run in workspace having docker-compose file.
13. **command** to override default command set in dockerfile.
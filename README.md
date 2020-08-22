# Docker Commands

- run - to run the image, if the image is not present it will download from the docker hub.
- run -d option - runs in background
- run -i option - interactive mode (for input)
- run -t option - terminal mode (for prompt)
- attach - to attach back to the background container.
- ps - it lists all the container running on the docker
- stop - to stop the container, give id or name of the container to stop
- rm - to remove the container
- images - to list the images
- rmi - to remove the image (make sure no container of this image is running)
- pull - to download the image and not run.
- exec - to execute a command on a running container e.g docker exec &lt;running container name or id> &lt;command to exec>

Containers are not made to run os. If you run ubuntu, it wil run and exit immediately. This is because, containers are made to run a specific process or task and not the os. If the task gets completed, it exits.

Port mapping : To access an application inside docker container. There are two ways
1. To use the ip address of the docker container, every docker has an ip address    	   associated with it. The port number is same as the port number of the application inside the docker. It is an internal ip which can be used by the docker host only.
2. Another way is to use the ip address of the host along with mapping the port number of the application with some other port number. This can be acheived using **-p newport : port** option with run.
3. Docker container has its own file system. To persist the data outside the container, map the directory outside the container. This can be achieved using **-v *outside container dir : inside container dir*** option with run command.
4. To get details of the container, use **inspect** command.
5. To view the logs, use **logs** command.
6. To set the environment variable in the container pass it with **-e key=value**.
7. To check the environment variable, run the inspect command.
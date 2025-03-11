# How to run a Docker container on a specific port?
When running a Docker container, you can map the container's internal port to a specific port on the host machine using the `-p` flag. <br>
`docker run -p <host_port>:<container_port> my-image` <br>

Where: <br>
- <host_port> is the port on the host machine (i.e. your computer). <br>
- <container_port> is the port on the container (inside Docker). <br>

# How to run two different Docker images of the same Spring Boot application on separate ports locally?
You can run multiple instances of the same Spring Boot application locally on Docker by binding each container to a different host port (or your computer's port). <br>
This allows you to access them independently via different localhost ports.

- Step 1: Build Two Different Docker Images <br>
If you have made different changes to each version of your Spring Boot application, build two separate images with different tags. <br>

> Build Image 1 (First Version)
>> `docker build -t my-spring-boot-app:v1 .`

> Build Image 2 (Second Version with changes)
>> `docker build -t my-spring-boot-app:v2 .`

- Step 2: Run Two Docker Containers <br>
Since both images expose the same internal port (8080), you must map them to different host ports: <br>
> `docker run -d -p 8081:8080 my-spring-boot-app:v1` <br>
> `docker run -d -p 8082:8080 my-spring-boot-app:v2` <br>

- Step 3: Access the Applications <br>
You can now access both versions of your Spring Boot application using the following URLs: <br>
> http://localhost:8081 <br>
> http://localhost:8082 <br>


# How to name a Docker container when running it?
When running a Docker container, you can specify a name for the container using the `--name` flag. This allows you to easily identify and manage the container later on. <br>
`docker run -d --name spring-app-v1 -p 8081:8080 my-spring-boot-app:v1` <br>
`docker run -d --name spring-app-v2 -p 8082:8080 my-spring-boot-app:v2` <br>

# What is a detached mode in Docker? How to run a docker container in detached mode?
Detached mode (-d) allows a Docker container to run in the background, without tying/blocking up your terminal. This means the container keeps running even if you close the terminal session. <br>
To run a container in detached mode: <br>
`docker run -d my-image` <br>

Therefore, the application runs in the background, and the terminal remains free. <br>
Without -d, Docker logs continuously print in the terminal, making it harder to run other commands. <br>
With -d, you can run other commands in the terminal while the container runs in the background. You can still access the logs of the container using `docker logs container-id`. <br>

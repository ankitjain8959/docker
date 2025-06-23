# Docker
Docker is a tool that helps developers package their applications along with everything they need to run—code, libraries, dependencies—into a single container (or, a lightweight & standalone package). <br>
This container can then be run on any machine that has Docker installed, regardless of the customized settings of the machine. <br>

# Containers vs Virtual Machines
A Container is a `self-contained package` (as it includes the application code, runtime, libraries, and dependencies) & `an isolated execution environment` (as it runs separately from the host system, ensuring consistency across different machines). <br>

A Virtual Machine (VM) is a software-based computer that runs inside another physical computer. It behaves like a real computer with its own operating system (OS), CPU, memory, and storage, but it shares the underlying hardware with other VMs. <br>

Benefits (examples) of using VMs:
- You can run Windows, Linux, and macOS on the same physical machine. <br>
- You can run multiple VMs on the same physical machine. <br>
- You can run different applications on different VMs. <br>

Containers are similar to virtual machines, but
- Containers are more `lightweight` (uses less memory) and `faster` (starts in seconds) than virtual machines <br>
- Containers are more `portable` than virtual machines, as they can be run on any machine that has Docker installed, regardless of the customized settings of the machine. <br>
- Containers are `consistent` across different environments (works the same in development, testing and production environments), which makes them easier to manage and deploy. <br>
- Containers share the host machine's operating system kernel, which makes them more efficient than virtual machines, which run their own operating system kernel. <br>
- Containers are also more `flexible` than virtual machines, as they can be easily scaled up or down, and can be used to run multiple applications on a single host machine. <br>

# The Docker Platform
Docker is a platform (set of tools & technologies) that helps developers build, package, run, and manage containers easily. <br>
It provides everything needed to develop, ship, and deploy applications in a containerized environment. <br>

## Key Components of the Docker Platform
1️⃣ Docker Engine 🛠️
- The core runtime that allows you to build and run containers. <br>
- It includes the Docker daemon, which manages containers. <br>

2️⃣ Docker CLI (Command-Line Interface) 💻
- A tool that lets you interact with Docker using commands (docker run, docker build, docker ps, etc.). <br>

3️⃣ Docker Hub 🌐
- A cloud-based registry where you can store and share container images. <br>
- You can pull official images like nginx, mysql, openjdk, or push your own. <br>

4️⃣ Docker Compose 📜
- A tool to define and run multi-container applications using a `docker-compose.yml` file. <br>
  Example: Running a web app with a database in a single command.

5️⃣ Docker Swarm (Orchestration) ⚖️ (Legacy, now mostly replaced by Kubernetes)
- A tool for managing multiple Docker containers across multiple machines. <br>
- Helps with scaling applications. <br>

6️⃣ Docker Desktop 🖥️
- A GUI-based tool for running Docker on Windows and macOS. <br>

# The Underlying Technology
- Docker is written in Go and takes advantage of several features of the Linux kernel to deliver its functionality. <br>
- Docker uses a technology called `namespaces` (a linux feature) to provide the isolated workspace called the container. When you run a container, Docker creates a set of namespaces for that container. <br>

# Benefits of Docker
- Docker ensures that your application runs the same way on any machine — your laptop, a server, or the cloud. <br>
✅ No more `It works on my machine!` issues <br>
✅ Package all dependencies into a container <br>
✅ Works across Windows, macOS, and Linux <br>

- Docker is perfect for microservices, where each service runs in its own container. <br>
- Docker works with Kubernetes, an open-source container orchestration platform, to manage and scale containers. It deploys more containers as demand increases. <br>

## Example use cases of Docker
Instead of installing databases and tools directly on your machine, run them in Docker! <br>


# Docker architecture
Docker uses a client-server architecture. <br>
Key Components of Docker Architecture: <br>
1️⃣ Docker Client: The command-line tool that allows users to interact with Docker. <br>
- The Docker client (docker) is the primary way that many Docker users interact with Docker. <br>
- When you use commands such as `docker run`, the client sends these commands to `dockerd`, which carries them out. The `docker` command uses the Docker API. <br>

2️⃣ Docker Daemon: The background service that manages the containers. <br>
- The Docker `daemon` (dockerd) listens for Docker API requests and manages Docker objects such as images, containers, networks, and volumes. <br>

3️⃣ Docker Registry: A repository for Docker images. <br>
- Docker Hub is a public registry that anyone can use, and Docker looks for images on Docker Hub by default. <br>
 - When you use the `docker pull` or `docker run` commands, Docker pulls the required images from your configured registry (Docker Hub, by default). <br>
- When you use the `docker push` command, Docker pushes your image to your configured registry (Docker Hub, by default). <br>

![Docker-architecture](images/Docker-architecture.png)


# Docker Objects
When you use Docker, you are creating and using images, containers, networks, volumes, plugins, and other objects. <br>

1️⃣ Images: A template or blueprint for creating containers. <br>
- Images are read-only templates that contain a set of instructions for creating a container.
- It contains the application code, runtime, libraries, and dependencies needed to run the application. <br>
- Docker images are created with the `docker build` command and are stored in a Docker registry. <br>
> Example: Think of an image like a baking recipe. It contains all the ingredients and instructions needed to bake a cake. <br>

2️⃣ Containers: Runnable instances of an image. <br>
- Containers are the running instances of an image. 
- It contains the same application and all it's dependencies, but now it's running and can be interacted with. <br>
- Docker containers are created with the `docker run` command. <br>
> Example: Think of a container like a cake that you baked using a recipe. The cake is the actual thing you can eat, while the recipe is just a set of instructions. <br>

3️⃣ Networks: Connect containers. <br>
- Networks are used to enable communication between containers. <br>
- Networks connect containers and the outside world. <br>
- Docker Networks are created with the `docker network` command. <br>
> Example: Think of a network like a road that connects various buildings (containers) in a city. It allows people (data) to move between buildings (containers). <br>

4️⃣ Volumes: Persist data. <br>
- Volumes are used to store data generated by and used by containers <br>
- Volumes persist data even after the container is stopped or deleted <br>
- To store data (like databases, logs or application files) in volumes
`docker run -v my-volume:/data my-app`
> Example: Think of a volume like a hard drive that stores data. It can be attached to a container to store data generated by the container. <br>

5️⃣ Plugins: Extend Docker functionality. <br>
- Plugins are used to extend Docker functionality. <br>
- Docker plugins are used to add new features to Docker, such as volume drivers, network drivers, and logging drivers. <br>
- Plugins can be installed `docker plugin install plugin-name` <br>

## How Docker Objects Work Together
- Create an `image` that has everything needed for your app.
- Run a `container` from that image, which executes your app.
- If your container needs to communicate with others, it joins a `network`.
- For data persistence, use `volumes` to store important data that survives container restarts.

# Build Image & Run Container
- To build a docker image: `docker build -t my-image .`
- To run a docker container: `docker run my-image`
- To run a docker container on a specific port: `docker run -p <host_port>:<container_port> my-image`

**<host_port>** is the port on the host machine (i.e. your computer). <br>
**<container_port**> is the port on the container (inside Docker). <br>
`-p 8080:8080` maps port 8080 on the host machine to port 8080 on the container. <br>
Since Spring Boot applications typically run on port 8080, this mapping allows external access to the application running inside the container.

- To run a docker container in detached mode (i.e. in the background, without blocking the terminal and container keeps running even if you close the terminal session): `docker run -d my-image`
  
# Docker Cheat Sheet
> Docker process command
- To list running containers: `docker ps`
- To list all containers: `docker ps -a`

> Docker format command
- To customize the output of the `docker ps` command: `docker ps --format "FORMAT_STRING"` <br>
For example, to display only the container ID and name in the output, you can use: <br>
docker ps --format "ID: {{.ID}}\tName: {{.Names}}"

> Docker image command
- To list images: `docker images`

> Docker remove command
- To remove a container: `docker rm container-id`
- To remove an image: `docker rmi image-id`

> Docker pull/push command
- To pull an image from Docker Hub: `docker pull image-name`
- To push an image to Docker Hub: `docker push image-name`

> Docker build/run command
- To build a docker image: `docker build -t my-image .`
- To run a docker container: `docker run my-image`
- To run a docker container in detached mode: `docker run -d my-image`
- To run a docker container on a specific port: `docker run -p <host_port>:<container_port> my-image`
- To run a docker container in detached mode on a specific port and connect to a network: `docker run --name my-mongo --network mynetwork -d -p 27017:27017 mongo`

> Docker start/stop command
- To start a container: `docker start container-id`
- To stop a container: `docker stop container-id`

> Docker create network command
- To create a network: `docker network create mynetwork`
- To list all networks: `docker network ls`

> Docker logs command
- To see logs/output of a container: `docker logs container-id`
- To see & follow logs/output in real time of a container: `docker logs -f container-id`

> Docker inspect command
- To inspect a container (i.e. to see low-level information about Docker objects): `docker inspect container-id`

> Docker exec command
- To run a command in a running container: `docker exec container-id ls`
- To run a command in a running container in interactive mode: `docker exec -it container-id /bin/bash`
- To run a command in a running container in interactive mode: `docker exec -it container-id /bin/sh`

  > Docker login/logout command
- To log in to Docker Hub: `docker login`
- To log in to a specific registry: `docker login registry-url`
- To log in to a registry with a username: `docker login -u username registry-url`
- To log in to a registry with a username and password: `docker login -u username -p password registry-url` <br>
  Note: It's recommended to use a token instead of a password for security reasons.

- To log out from Docker Hub: `docker logout`
- To log out from a specific registry: `docker logout registry-url`

# Docker Compose (Tool)
- A tool to define and run multi-container applications.
- It uses a `docker-compose.yml` file (or, just `compose.yaml` file starting Docker compose v2 version) to configure your application’s services like databases, backend, frontend, etc.
- It simplifies container management by allowing you to define all services in a single file and run them together with one command.

```
Instead of running separate `docker run` commands for each container manually — like for my Spring Boot app, MongoDB, etc. — we can use Docker Compose to define all of them in a single YAML file `compose.yaml`.
Then, with just one command `docker compose up`, we can build, configure, and run all the services together in a consistent, repeatable way.
```

Example of a `docker-compose.yml` file that is equivalent to the below `docker run` command to start a MongoDB container:
```start mongodb
docker run -d \
    -p 27017:27017 \
    -e MONGO_INITDB_ROOT_USERNAME=admin \
    -e MONGO_INITDB_ROOT_PASSWORD=admin \
    --network mongo-network \
    --name mongodb \
    mongo
```
[compose-mongodb.yaml](src/compose-mongodb.yaml)

- By default, Docker Compose sets up a network for the containers to communicate with each other even if you don't create it and mention it in the compose yaml file <br>
- To control the order of service startup & shutdown, use the `depends_on` option in the `compose.yml` file. <br>

## Docker Compose Commands
- To start containers/services defined in the `docker-compose.yml` or `compose.yml` file & in detached mode: `docker compose up -d`
- To start containers/services defined in a custom `compose-custom.yml` file: `docker-compose -f compose-custom.yml up -d`

- To stop containers/services defined in the `compose.yml` file: `docker compose stop`
- To stop containers/services defined in a custom `compose-custom.yml` file: `docker-compose -f compose-custom.yml stop`

- To stop & remove containers/services, networks, volumes and images defined in the `compose.yml` file: `docker compose down`
- To stop & remove containers/services, networks, volumes and images defined in a custom `compose-custom.yml` file: `docker-compose -f compose-custom.yml down`
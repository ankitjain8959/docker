# Docker
Docker is a tool that helps developers package their applications along with everything they need to run—code, libraries, dependencies—into a single container (or, a lightweight & standalone package). <br>
This container can then be run on any machine that has Docker installed, regardless of the customized settings of the machine. <br>

## Containers vs Virtual Machines
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
- A tool to define and run multi-container applications using a docker-compose.yml file. <br>
  Example: Running a web app with a database in a single command.

5️⃣ Docker Swarm (Orchestration) ⚖️ (Legacy, now mostly replaced by Kubernetes)
- A tool for managing multiple Docker containers across multiple machines. <br>
- Helps with scaling applications. <br>

6️⃣ Docker Desktop 🖥️
- A GUI-based tool for running Docker on Windows and macOS. <br>

# The Underlying Technology
- Docker is written in Go and takes advantage of several features of the Linux kernel to deliver its functionality. <br>
- Docker uses a technology called `namespaces` (a linux feature) to provide the isolated workspace called the container. When you run a container, Docker creates a set of namespaces for that container. <br>

## Benefits of Docker
- Docker ensures that your application runs the same way on any machine—your laptop, a server, or the cloud. <br>
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

![Docker-architecture](Docker-architecture.png)


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
- To list running containers: `docker ps`
- To list all containers: `docker ps -a`

- To list images: `docker images`

- To remove a container: `docker rm container-id`
- To remove an image: `docker rmi image-id`

- To pull an image from Docker Hub: `docker pull image-name`
- To push an image to Docker Hub: `docker push image-name`

- To build a docker image: `docker build -t my-image .`
- To run a docker container: `docker run my-image`
- To run a docker container in detached mode: `docker run -d my-image`
- To run a docker container on a specific port: `docker run -p <host_port>:<container_port> my-image`

- To start a container: `docker start container-id`
- To stop a container: `docker stop container-id`

- To see logs of a container: `docker logs container-id`
- To see & follow logs in real time of a container: `docker logs -f container-id`

# Next: Docker Compose

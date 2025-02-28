# Docker Notes for DevOps Beginners

## Introduction to Docker

### Virtualization vs Containerization
- **VirtualBox**: Used to run Linux on Windows (Full OS Virtualization)
  - Costly
  - Requires more resources
- **Docker (Containerization)**:
  - More cost-effective than VirtualBox
  - Runs on top of the OS as a **Docker Engine**
  - Talks directly to the **kernel**, creates **containers**, and uses **shared resources**

### Docker Components
- **Docker**: The core containerization tool
- **containerd**: The heart of Docker responsible for container execution
- **dockerd**: A background process that manages containerd
- **Docker CLI**: Interface to interact with Docker
- **Docker Client**: Used to send commands to Docker
- **Docker App**: A container engine to manage applications

## Basic Docker Commands
```sh
# Show running containers
$ docker ps
```

### Fixing Permission Issues
If you see **permission denied**, check the Docker group:
```sh
$ cat /etc/group
```
If Docker does not have a group, add the current user:
```sh
$ sudo usermod -aG docker $USER
$ newgrp docker  # Refresh the group permissions
```

## Creating Docker Containers
### Method 1: Using a Dockerfile
1. **Create a Dockerfile** to define the container image (acts as a blueprint)
2. **Build the image** from the Dockerfile
3. **Run the container** using the created image

### Method 2: Pulling an Image from Docker Hub
1. **Pull an image** directly from Docker Hub
2. **Run the container** using the pulled image

## Running a Docker Container
```sh
# Run a basic Ubuntu container interactively
$ docker run -it ubuntu

# Run an Nginx container with port mapping
$ docker run -p 80:80 nginx

# List all running containers (including stopped ones)
$ docker ps -a
```

### Running Containers in the Background
```sh
# Run a container in detached mode
$ docker run -d -p 80:80 my-app
```

## Understanding Builds in Docker
- **Build Process**: Compilation of code into an executable application
- Different languages have different build tools:
  - **.NET** → MSBuild
  - **Java** → Maven
  - **Node.js** → npm
  - **Python** → pip

## Creating a Dockerfile
### Syntax:
```dockerfile
# Base image
FROM ubuntu:latest

# Set working directory
WORKDIR /app

# Copy application files
COPY foldername/filename /tofile/filename

# Install dependencies or compile code
RUN javac Main.java

# Expose a port (optional)
EXPOSE 8080

# Command to run application
CMD ["java", "Main"]
```

## Running Docker Commands
```sh
# Build an image
$ docker build -t my-image:latest .

# List Docker images
$ docker images

# Run the container from an image
$ docker run -d -p 80:80 my-app

# Stop a running container
$ docker stop <container-id>

# Remove a stopped container
$ docker rm <container-id>

# View container logs
$ docker logs <container-id>

# Clean up unused containers and images
$ docker system prune
```

### Important Note
Whenever you **modify or add new code**, you **must rebuild** the Dockerfile:
```sh
$ docker build -t my-image:latest .
```


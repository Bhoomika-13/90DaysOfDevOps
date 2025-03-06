# Docker Notes for DevOps (Basic to Advanced)

## **Introduction to Docker**
Docker is a **containerization** platform that enables developers to package applications and their dependencies into isolated environments known as containers.

### **Virtualization vs. Containerization**
- **Virtualization** (e.g., VirtualBox): Runs an entire OS on top of another OS, which is resource-heavy.
- **Containerization** (e.g., Docker): Shares the host OS kernel, making it lightweight and efficient.

### **Docker Architecture**
1. **Docker Engine** - Runs on the OS to create and manage containers.
2. **Containerd** - The core container runtime that manages the lifecycle of containers.
3. **Docker Daemon (dockerd)** - Background process that communicates with containerd.
4. **Docker CLI** - Command-line interface to interact with Docker.
5. **Docker Client** - Used to manage and communicate with Docker Daemon.

---

## **Docker Basic Commands**
### **Checking Docker Status**
```sh
docker ps        # Shows running containers
docker ps -a     # Shows all containers (running + stopped)
```

### **Fixing Permission Issues**
```sh
sudo usermod -aG docker $USER  # Add current user to the Docker group
newgrp docker                   # Refresh group membership
```

### **Creating Docker Containers**
#### **Method 1: Using a Dockerfile**
1. **Create a Dockerfile:**
```Dockerfile
FROM ubuntu:latest
WORKDIR /app
COPY . /app
RUN apt-get update && apt-get install -y python3
CMD ["python3", "app.py"]
```
2. **Build and run the container:**
```sh
docker build -t myapp:latest .
docker run -d -p 8080:80 myapp:latest
```

#### **Method 2: Without a Dockerfile**
```sh
docker pull nginx  # Pull image from Docker Hub
docker run -p 80:80 nginx  # Run container
```

### **Stopping and Removing Containers**
```sh
docker stop <container_id>  # Stop a running container
docker rm <container_id>    # Remove a stopped container
docker system prune -a      # Remove all stopped containers and images
```

---

## **Building and Managing Docker Images**
```sh
docker build -t myapp:v1 .      # Build an image
docker images                   # List all images
docker rmi <image_id>           # Remove an image
docker tag myapp:v1 myrepo/myapp:v1  # Tag an image
docker push myrepo/myapp:v1      # Push image to Docker Hub
```

---

## **Multi-Stage Docker Builds**
Multi-stage builds allow for smaller and more secure images.

### **Example:**
```Dockerfile
# Stage 1: Build dependencies
FROM python:3.9-slim AS builder
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt --target=/app/deps

# Stage 2: Minimal runtime image
FROM gcr.io/distroless/python3-debian12
WORKDIR /app
COPY --from=builder /app/deps /app/deps
COPY --from=builder /app .
ENV PYTHONPATH="/app/deps"
CMD ["python3", "app.py"]
```
**Building the Multi-Stage Image:**
```sh
docker build -t python-app-mini .
```

---

## **Docker Networking**
### **Types of Docker Networks:**
1. **Bridge (default)** - Connects containers via an internal network.
2. **Host** - Uses the host’s network (no port mapping required).
3. **None** - Completely isolated.
4. **User-defined Bridge** - Custom network with better container communication.
5. **Macvlan** - Assigns a MAC address to a container for direct host communication.
6. **Overlay** - Used in Docker Swarm for multi-host networking.

### **Docker Networking Commands**
```sh
docker network ls       # List networks
docker network inspect <network_id>  # Inspect network
docker network create my_network  # Create a custom network
docker run --network=my_network nginx  # Attach container to a network
```

---

## **Docker Volumes (Persistent Storage)**
Volumes are used to store data outside of containers.

```sh
docker volume create my_volume  # Create a volume
docker volume ls                # List volumes
docker run -d -v my_volume:/data mysql  # Attach volume to a container
docker volume inspect my_volume  # Get volume details
```

---

## **Pushing and Pulling Docker Images**
```sh
docker login
# Tag and push image

docker tag myapp:v1 mydockerhubusername/myapp:v1
docker push mydockerhubusername/myapp:v1

docker pull mydockerhubusername/myapp:v1  # Pull from Docker Hub
```

Docker Compose: Simplifying Container Management

What is Docker Compose?

Docker Compose is a tool that helps you build images and run containers using a single YAML configuration file (docker-compose.yml). It allows you to define multiple services, manage dependencies, set up networking, and automate container startup.

YAML File Basics

YAML (.yml) is a configuration file format that uses key-value pairs and objects to define services, networks, and volumes.

Basic Structure of docker-compose.yml

version: '3.8'  # Define the Docker Compose version

services:   # Define all container services here

  mysql:
    image: mysql:5.7   # Use MySQL version 5.7
    container_name: mysql
    environment:  # Set up database environment variables
      MYSQL_ROOT_PASSWORD: admin
      MYSQL_USER: admin
      MYSQL_PASSWORD: admin
      MYSQL_DATABASE: tws_db
    volumes:
      - ./mysql_data_new:/var/lib/mysql  # Persistent storage for MySQL
    networks:
      - twotier
    ports:
      - "3306:3306"  # Map MySQL port
    healthcheck:  # Ensure MySQL is ready before dependent services start
      test: ["CMD", "mysqladmin", "ping", "-h", "localhost", "-uroot", "-padmin"]
      interval: 10s
      retries: 5
      start_period: 60s
      timeout: 5s

  flaskapp:
    build:  # Build the Flask app if no image exists
      context: .  # Use the Dockerfile in the same directory
    container_name: flaskapp
    environment:
      MYSQL_PASSWORD: admin
      MYSQL_USER: root
      MYSQL_HOST: mysql
      MYSQL_DB: tws_db
    networks:
      - twotier
    ports:
      - "5000:5000"  # Expose Flask app on port 5000
    depends_on:  # Ensure MySQL starts before Flask
      - mysql
    restart: always  # Restart the container on failure

volumes:
  mysql_data_new:  # Define persistent volume for MySQL

networks:
  twotier:  # Define a custom bridge network


Common Docker Compose Commands

Command

Description

docker compose up -d

Start all services in detached mode

docker compose down

Stop and remove all containers

docker compose ps

List running containers

docker compose logs -f

View live logs

docker compose restart service_name

Restart a specific service

docker compose exec service_name bash

Access the container’s shell

Important Notes

✔ If you fix errors or modify the configuration, stop the container using:
🔹 docker compose down before restarting with docker compose up -d.

✔ Install Docker Compose (if not installed):
🔹 sudo apt-get install docker-compose

✔ Docker Scout can be used for image security analysis:
🔹 docker scout quickview image_name

This setup ensures automatic dependency management, persistent storage, and smooth orchestration of multiple services in a two-tier application. 🚀

Let me know if you need any refinements! 😊Docker Compose: Simplifying Container Managemen

What is Docker Compose?

Docker Compose is a tool that helps you build images and run containers using a single YAML configuration file (docker-compose.yml). It allows you to define multiple services, manage dependencies, set up networking, and automate container startup.

YAML File Basics

YAML (.yml) is a configuration file format that uses key-value pairs and objects to define services, networks, and volumes.

Basic Structure of docker-compose.yml

version: '3.8'  # Define the Docker Compose version

services:   # Define all container services here

  mysql:
    image: mysql:5.7   # Use MySQL version 5.7
    container_name: mysql
    environment:  # Set up database environment variables
      MYSQL_ROOT_PASSWORD: admin
      MYSQL_USER: admin
      MYSQL_PASSWORD: admin
      MYSQL_DATABASE: tws_db
    volumes:
      - ./mysql_data_new:/var/lib/mysql  # Persistent storage for MySQL
    networks:
      - twotier
    ports:
      - "3306:3306"  # Map MySQL port
    healthcheck:  # Ensure MySQL is ready before dependent services start
      test: ["CMD", "mysqladmin", "ping", "-h", "localhost", "-uroot", "-padmin"]
      interval: 10s
      retries: 5
      start_period: 60s
      timeout: 5s

  flaskapp:
    build:  # Build the Flask app if no image exists
      context: .  # Use the Dockerfile in the same directory
    container_name: flaskapp
    environment:
      MYSQL_PASSWORD: admin
      MYSQL_USER: root
      MYSQL_HOST: mysql
      MYSQL_DB: tws_db
    networks:
      - twotier
    ports:
      - "5000:5000"  # Expose Flask app on port 5000
    depends_on:  # Ensure MySQL starts before Flask
      - mysql
    restart: always  # Restart the container on failure

volumes:
  mysql_data_new:  # Define persistent volume for MySQL

networks:
  twotier:  # Define a custom bridge network


Common Docker Compose Commands

Command

Description

docker compose up -d

Start all services in detached mode

docker compose down

Stop and remove all containers

docker compose ps

List running containers

docker compose logs -f

View live logs

docker compose restart service_name

Restart a specific service

docker compose exec service_name bash

Access the container’s shell

Important Notes

✔ If you fix errors or modify the configuration, stop the container using:
🔹 docker compose down before restarting with docker compose up -d.

✔ Install Docker Compose (if not installed):
🔹 sudo apt-get install docker-compose

✔ Docker Scout can be used for image security analysis:
🔹 docker scout quickview image_name


---

## **Advanced Docker Commands**
```sh
docker ps -aq           # Get all container IDs
docker rm $(docker ps -aq)  # Remove all stopped containers
docker images -aq       # Get all image IDs
docker rmi $(docker images -aq)  # Remove all images
```

---




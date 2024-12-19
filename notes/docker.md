## Docker Cheat Sheet

### Basic Docker Commands

```bash
# List all running containers
docker ps

# Start a container
docker start <container_id>

# Stop a container
docker stop <container_id>

# Remove a container
docker rm <container_id>

# Build an image from a Dockerfile
docker build -t <image_name> .

# Run a container from an image
docker run -d -p 8080:80 <image_name>

# View logs of a container
docker logs <container_id>

# List all images
docker images

# Remove an image
docker rmi <image_id>

# Start an interactive terminal inside a running container
docker exec -it <container_id> /bin/bash
```

### Docker Cleanup

```bash

# Remove all stopped containers
docker container prune

# Remove all unused images
docker image prune -a

# Remove all unused networks
docker network prune

# Remove all dangling volumes
docker volume prune

# Remove all docker builds
docker builder prune

```

### Docker File Instructions

```bash
# Specify base image
FROM node:14

# Set the working directory in the container
WORKDIR /app

# Copy package.json into the working directory
COPY package.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

# Expose port 3000
EXPOSE 3000

# Command to run the application
CMD ["npm", "start"]

```

### Image and Container Management

```bash

# Tag an image with a specific version
docker tag <image_name> <repository>/<image_name>:<tag>

# Push an image to a Docker registry
docker push <repository>/<image_name>:<tag>

# Pull an image from a Docker registry
docker pull <repository>/<image_name>:<tag>

# Remove all stopped containers
docker container prune

# Remove all dangling images (images not tagged and not used by any container)
docker image prune
```

### Docker Volumes (for persistent data)

```bash

# Create a new volume
docker volume create <volume_name>

# List all volumes
docker volume ls

# Mount a volume to a container
docker run -d -p 8080:80 -v <volume_name>:/path/in/container <image_name>

# Inspect a volume
docker volume inspect <volume_name>

# Remove a volume
docker volume rm <volume_name>
```

### Docker Compose

```bash
# Example docker-compose.yml file
version: '3'
services:
  web:
    image: node:14
    working_dir: /app
    volumes:
      - .:/app
    ports:
      - "3000:3000"
    command: npm start
  db:
    image: postgres:12
    environment:
      POSTGRES_USER: example
      POSTGRES_PASSWORD: example
      POSTGRES_DB: exampledb
    ports:
      - "5432:5432"

```

### Run Docker Compose

```bash
# Build and start all services defined in docker-compose.yml in detached mode
docker-compose up --build -d

# Start services without rebuilding images
docker-compose up -d

# Start services and display logs in real-time
docker-compose up

# Rebuild a specific service and run it in detached mode
docker-compose up --build -d <service_name>

# Start services with a specific docker-compose file (other than the default docker-compose.yml)
docker-compose -f <custom-compose-file.yml> up -d

# Scale a specific service to run multiple instances (e.g., 3 instances of 'web')
docker-compose up -d --scale web=3

# Start services, forcing the removal of orphaned containers (services removed from the compose file)
docker-compose up -d --remove-orphans

# Recreate containers even if they have not changed
docker-compose up --force-recreate -d

```

### Docker Network

```bash
# Inspect the list of active networks
docker network ls

# Create a network
docker network create shared-network # sample network name

# Manually connect  mysql image to shared network
docker network connect shared-network mysql

# Network inspect
docker network inspect shared-network

```

### Useful Tips

```bash

# Build and tag an image in one command
docker build -t <repository>/<image_name>:<tag> .

# Restart a container
docker restart <container_id>

# Run a container and remove it after it stops
docker run --rm <image_name>

# Stop all running containers
docker stop $(docker ps -q)

# Remove all containers (stopped and running)
docker rm $(docker ps -aq)

# Access the container shell
docker exec -it <mysql_container_id> bash

# Once inside the container, use the MySQL CLI to connect
mysql -u root -p
```

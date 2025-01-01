2025-01-01 19:25

Status:

Tags:


# Docker


- To get IP address of container
```shell
docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' <container_name>
```


### 1. Docker-File :
It contains code to build our docker image.

### 2. Docker Commands :

**Image Commands:**

1. `docker build -t <image-name> <path>`: Build a Docker image from a Docker-file.
2. `docker images`: List all available Docker images.
3. `docker rmi <image-name>`: Remove a Docker image.

**Container Commands:**

1. `docker run <options> <image-name>`: Run a new container from an image.
2. `docker ps`: List running containers.
3. `docker ps -a`: List all containers (including stopped ones).
4. `docker start <container-id/name>`: Start a stopped container.
5. `docker stop <container-id/name>`: Stop a running container.
6. `docker restart <container-id/name>`: Restart a running or stopped container.
7. `docker rm <container-id/name>`: Remove a stopped container.
8. `docker exec -it <container-id/name> <command>`: Execute a command inside a running container.
9. `docker logs <container-id/name>`: Display logs of a container.

**Networking Commands:**

1. `docker network ls`: List Docker networks.
2. `docker network create <network-name>`: Create a Docker network.
3. `docker network connect <network-name> <container-id/name>`: Connect a container to a network.
4. `docker network disconnect <network-name> <container-id/name>`: Disconnect a container from a network.
5. `docker port <container-id/name>`: Show public-facing port of a container.

**Volume Commands:**

1. `docker volume ls`: List Docker volumes.
2. `docker volume create <volume-name>`: Create a Docker volume.
3. `docker volume inspect <volume-name>`: Inspect details of a volume.
4. `docker volume rm <volume-name>`: Remove a Docker volume.
5. `docker run -v <volume-name>:<container-path> <image-name>`: Mount a volume to a container.

**Registry & Repository Commands:**

1. `docker pull <image-name>`: Pull an image from a Docker registry.
2. `docker push <image-name>`: Push an image to a Docker registry.
3. `docker login`: Log in to a Docker registry.

**Other Useful Commands:**

1. `docker info`: Display Docker system information.
2. `docker version`: Display Docker version information.
3. `docker-compose`: Manage multi-container applications using Compose.
4. `docker system prune`: Remove all unused containers, networks, and images to reclaim space.

Remember to replace `<options>`, `<image-name>`, `<container-id/name>`, `<network-name>`, and `<volume-name>` with appropriate values in the commands. You can use `docker --help` or `docker <command> --help` for more detailed information on each command.

### 3. More commands :

1. The `docker buildx create` command is used to create a new builder instance. The `--name` flag is used to specify the name of the builder instance. The `--use` flag is used to switch to the specified builder instance. `docker buildx create --name mybuilder --use` Image created using buildx will remain in cache only so need to push directly from the same command
```shell
// Use docker buildx to build different platform images 
docker buildx create --name mybuilder --use

// Important: add http:// to the url which I forgot when you set --build-arg api_base_ur 
docker buildx build --platform linux/amd64,linux/arm64 . \
-t shreyas957/shreyas-full-stack-professional-react \
--build-arg api_base_url=http://{url_of_env(1st lattter small)}:8080 \
--push
```

```

Format Docker ps Output :

```bash
export FORMAT="ID\\t{{.ID}}\\nNAME\\t{{.Names}}\\nImage\\t{{.Image}}\\nPORTS\\t{{.Ports}}\\nCOMMAND\\t{{.Command}}\\nCREATED\\t{{.CreatedAt}}\\nSTATUS\\t{{.Status}}\\n”
docker ps --format="$FORMAT"
```

### 4. Dockerfile :

Docker can build images automatically by reading the instructions from a `Dockerfile`. A `Dockerfile` is a text document that contains all the commands a user could call on the command line to assemble an image. This page describes the commands you can use in a `Dockerfile`.

```yaml
FROM node:19-alpine  # From which we are building img
ARG api_base_url
WORKDIR /app   # Set working directory
COPY package*.json .     # Copy package name starting files(* is used) into . (Working directory)
RUN npm i --silent
COPY . .   # copy everything into working directory
RUN echo "VITE_API_BASE_URL=${api_base_url}" > .env   # create .env file with the content given
EXPOSE 5173
CMD ["npm", "run", "dev"]

```

Using `dockerignore` we exclude node_modules, Dockerfile and .env files into our image.



# References

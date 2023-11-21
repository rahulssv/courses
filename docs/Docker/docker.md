# Docker
- **Docker** is a platform that enables developers to automate the deployment of applications inside lightweight, portable containers. 
- **Containers** are a form of virtualization that allows applications and their dependencies to be packaged together, ensuring consistency across different environments. 
- Docker containers encapsulate everything needed to run an application, including the code, runtime, libraries, and system tools.

Key components of Docker include:

- **Docker Engine**: The core of Docker, responsible for creating and managing containers.
- Docker Images: Containers are created from Docker images, which are lightweight, standalone, and executable packages that include application code, runtime, libraries, and system tools.

- **Dockerfile:** A text file that contains instructions for building a Docker image. It specifies the base image, application code, dependencies, and other configuration settings.

- **Docker Hub:** A cloud-based registry service that allows you to share and distribute Docker images. Docker Hub is also a repository of pre-built images that developers can use.

- **Docker Compose:** A tool for defining and running multi-container Docker applications. It uses a YAML file to configure the application's services, networks, and volumes.
  
## **Docker Management Commands:**

Certainly! Here are some Docker management commands along with examples:

### Docker Management Commands:

1. **Display Docker version information:**
    ```bash
    docker version
    ```

2. **Display system-wide Docker information:**
    ```bash
    docker info
    ```

3. **Show help for a specific command or general Docker help:**
    ```bash
    docker --help
    # or
    docker <command> --help
    # Example: docker run --help
    ```

## **Image Commands:**
Certainly! Here's a breakdown of Docker image commands with examples:

### Image Commands:

1. **List all images on the local machine:**
    ```bash
    docker images
    ```

2. **Search for an image on Docker Hub:**
    ```bash
    docker search <term>
    # Example: docker search ubuntu
    ```

3. **Download an image from Docker Hub:**
    ```bash
    docker pull <image>
    # Example: docker pull ubuntu:latest
    ```

4. **Build an image from a Dockerfile:**
    ```bash
    docker build -t <tag> <path>
    # Example: docker build -t my_image:latest .
    ```

5. **Show the history of an image, including its layers:**
    ```bash
    docker history <image>
    # Example: docker history ubuntu:latest
    ```

6. **Display detailed information about an image:**
    ```bash
    docker inspect <image>
    # Example: docker inspect my_image:latest
    ```

7. **Tag an image with a new name and optionally a new tag:**
    ```bash
    docker tag <source_image>:<source_tag> <target_image>:<target_tag>
    # Example: docker tag my_image:latest my_repository/my_image:1.0
    ```

8. **Remove one or more images:**
    ```bash
    docker rmi <image>
    # Example: docker rmi my_image:latest
    ```

9. **Remove all dangling images:**
    ```bash
    docker image prune
    ```

10. **Remove all unused images, not just dangling ones:**
    ```bash
    docker image prune -a
    ```

These commands cover a range of image-related tasks, from managing and inspecting images to searching for new ones on Docker Hub.

## **Container Commands:**
Certainly! Here's a breakdown of the Docker container commands with examples:

### Container Lifecycle:

1. **List running containers:**
    ```bash
    docker ps
    ```

2. **List all containers, including stopped ones:**
    ```bash
    docker ps -a
    ```

3. **Create and start a container from an image:**
    ```bash
    docker run <options> <image>
    # Example: docker run -it ubuntu:latest /bin/bash
    ```

4. **Start a stopped container:**
    ```bash
    docker start <container>
    # Example: docker start my_container
    ```

5. **Stop a running container:**
    ```bash
    docker stop <container>
    # Example: docker stop my_container
    ```

6. **Restart a container:**
    ```bash
    docker restart <container>
    # Example: docker restart my_container
    ```

7. **Pause all processes within a container:**
    ```bash
    docker pause <container>
    # Example: docker pause my_container
    ```

8. **Unpause a paused container:**
    ```bash
    docker unpause <container>
    # Example: docker unpause my_container
    ```

9. **Run a command in a running container:**
    ```bash
    docker exec -it <container> <command>
    # Example: docker exec -it my_container /bin/bash
    ```

10. **Attach to a running container's process:**
    ```bash
    docker attach <container>
    # Example: docker attach my_container
    ```

### Container Information:

11. **Display detailed information about a container:**
    ```bash
    docker inspect <container>
    # Example: docker inspect my_container
    ```

12. **Fetch the logs of a container:**
    ```bash
    docker logs <container>
    # Example: docker logs my_container
    ```

13. **Display the running processes of a container:**
    ```bash
    docker top <container>
    # Example: docker top my_container
    ```

14. **Display a live stream of container resource usage statistics:**
    ```bash
    docker stats <container>
    # Example: docker stats my_container
    ```

### Container Removal:

15. **Remove one or more containers:**
    ```bash
    docker rm <container>
    # Example: docker rm my_container
    ```

16. **Forcefully remove a running container:**
    ```bash
    docker rm -f <container>
    # Example: docker rm -f my_container
    ```

17. **Remove all stopped containers:**
    ```bash
    docker container prune
    ```

18. **Remove all containers forcefully:**
    ```bash
    docker rm $(docker ps -a -q)
    ```

### Copying Files:

19. **Copy files or directories between a container and the local filesystem:**
    ```bash
    docker cp <source_path> <container>:<destination_path>
    # Example: docker cp ./local_file.txt my_container:/app/
    ```

20. **Copy files or directories from a container to the local filesystem:**
    ```bash
    docker cp <container>:<source_path> <destination_path>
    # Example: docker cp my_container:/app/container_file.txt ./local_destination/
    ```

### Resource Management:

21. **Display a live stream of system resource usage statistics for all containers:**
    ```bash
    docker stats
    ```

22. **Update container resource limits:**
    ```bash
    docker update <container> --memory <limit>
    # Example: docker update my_container --memory 512m
    ```



## **Network Commands:**
Here are some Docker network commands along with examples:

### List Networks:

1. **`docker network ls`**: List all networks.

   ```bash
   docker network ls
   ```

2. **`docker network inspect <network>`**: Display detailed information about a network.

   ```bash
   docker network inspect bridge
   ```

### Create and Remove Networks:

3. **`docker network create <network>`**: Create a network.

   ```bash
   docker network create my_network
   ```

4. **`docker network rm <network>`**: Remove one or more networks.

   ```bash
   docker network rm my_network
   ```

### Connect Containers to Networks:

5. **`docker network connect <network> <container>`**: Connect a container to a network.

   ```bash
   docker network connect my_network my_container
   ```

6. **`docker network disconnect <network> <container>`**: Disconnect a container from a network.

   ```bash
   docker network disconnect my_network my_container
   ```

### Bridge Network:

7. **`docker network create --driver bridge <network>`**: Create a user-defined bridge network.

   ```bash
   docker network create --driver bridge my_bridge_network
   ```

### Host Network:

8. **`docker run --network host <image>`**: Run a container on the host's network stack.

   ```bash
   docker run --network host my_image
   ```

### Overlay Network (Swarm Mode):

9. **`docker network create --driver overlay <network>`**: Create an overlay network for Swarm services.

   ```bash
   docker network create --driver overlay my_overlay_network
   ```

### Macvlan Network:

10. **`docker network create --driver macvlan --subnet=<subnet> --gateway=<gateway> -o parent=<interface> <network>`**: Create a Macvlan network.

    ```bash
    docker network create --driver macvlan --subnet=192.168.1.0/24 --gateway=192.168.1.1 -o parent=eth0 my_macvlan_network
    ```

These are some common Docker network commands and examples. Docker provides various network drivers and options to suit different use cases, such as connecting containers within a host, connecting containers across hosts in a Swarm, or even creating custom bridge networks. Adjust the examples based on your specific requirements and network configurations.
## **Volume Commands:**
Here are some commonly used Docker volume commands:

1. **`docker volume create <volume>`**: Create a named volume.

   ```bash
   docker volume create my_volume
   ```

2. **`docker volume ls`**: List all volumes.

   ```bash
   docker volume ls
   ```

3. **`docker volume inspect <volume>`**: Display detailed information about a volume.

   ```bash
   docker volume inspect my_volume
   ```

4. **`docker volume rm <volume>`**: Remove one or more volumes.

   ```bash
   docker volume rm my_volume
   ```

5. **`docker volume prune`**: Remove all unused volumes.

   ```bash
   docker volume prune
   ```

These commands allow you to manage Docker volumes, which are used to persist data generated by and used by Docker containers. Volumes provide a way to share data between containers, and they exist independently of the container lifecycle, making data storage more durable and flexible.
## **Docker Compose Commands:**
Docker Compose is a tool for defining and running multi-container Docker applications. Here are some common Docker Compose commands along with examples:

### Basic Commands:

1. **`docker-compose up`**: Start services defined in a `docker-compose.yml` file.

    ```bash
    docker-compose up
    ```

2. **`docker-compose down`**: Stop and remove containers, networks, and volumes defined in a `docker-compose.yml` file.

    ```bash
    docker-compose down
    ```

3. **`docker-compose ps`**: List containers.

    ```bash
    docker-compose ps
    ```

### Service Management:

4. **`docker-compose start`**: Start services.

    ```bash
    docker-compose start
    ```

5. **`docker-compose stop`**: Stop services.

    ```bash
    docker-compose stop
    ```

6. **`docker-compose restart`**: Restart services.

    ```bash
    docker-compose restart
    ```

### Logs and Status:

7. **`docker-compose logs`**: View output from services.

    ```bash
    docker-compose logs
    ```

8. **`docker-compose top`**: Display the running processes.

    ```bash
    docker-compose top
    ```

### Scale Services:

9. **`docker-compose scale`**: Scale services to a specified number of instances.

    ```bash
    docker-compose scale web=3
    ```

### Executing Commands in Services:

10. **`docker-compose exec`**: Run a command in a service.

    ```bash
    docker-compose exec web ls -l
    ```

### Building and Rebuilding:

11. **`docker-compose build`**: Build or rebuild services.

    ```bash
    docker-compose build
    ```

12. **`docker-compose pull`**: Pull service images.

    ```bash
    docker-compose pull
    ```

### Managing Networks and Volumes:

13. **`docker-compose network ls`**: List networks.

    ```bash
    docker-compose network ls
    ```

14. **`docker-compose volume ls`**: List volumes.

    ```bash
    docker-compose volume ls
    ```

### Other Commands:

15. **`docker-compose config`**: Validate and view the compose file.

    ```bash
    docker-compose config
    ```

16. **`docker-compose events`**: Receive real-time events from services.

    ```bash
    docker-compose events
    ```

These are some common Docker Compose commands, but there are more options and variations available. Always refer to the official Docker Compose documentation for the most up-to-date and detailed information: [Docker Compose CLI documentation](https://docs.docker.com/compose/reference/).
## **System Commands:**

### Docker System Information:

1. **`docker version`**
   - Example: `docker version`

2. **`docker info`**
   - Example: `docker info`

### Docker System Management:

3. **`docker system df`**
   - Example: `docker system df`

4. **`docker system prune`**
   - Example: `docker system prune`
   - This command can be used to remove unused data such as stopped containers, networks not used by any container, dangling images, and build cache.

5. **`docker system prune -a`**
   - Example: `docker system prune -a`
   - This variant of the `prune` command removes all unused containers, networks, and images not just dangling ones.

### Docker System Events:

6. **`docker events`**
   - Example: `docker events`
   - This command displays real-time events from the server.

### Docker System Shell Access:

7. **`docker system exec -it <container> <command>`**
   - Example: `docker exec -it my_container sh`
   - This allows you to execute a command inside a running container.

### Docker System Diagnostics:

8. **`docker system diagnose`**
   - Example: `docker system diagnose`
   - This command collects system information for Docker troubleshooting purposes.

### Docker System Cleanup:

9. **`docker system prune --volumes`**
   - Example: `docker system prune --volumes`
   - This variant of the `prune` command also removes volumes.

These commands provide information about the Docker system, help manage resources, and perform various maintenance tasks. Always refer to the official Docker documentation for the most up-to-date information and additional details on each command: [Docker CLI documentation](https://docs.docker.com/engine/reference/commandline/).
## **Registry/Login Commands:**
Docker provides commands for working with container registries, especially for logging in and out of container registries. Here are the main Docker registry/login commands along with examples:

1. **`docker login`**: Log in to a Docker registry.

   ```bash
   docker login [OPTIONS] [SERVER]
   ```

   - Example:
     ```bash
     docker login myregistry.example.com
     ```

   This command prompts you for a username and password to authenticate with the specified Docker registry.

2. **`docker logout`**: Log out from a Docker registry.

   ```bash
   docker logout [SERVER]
   ```

   - Example:
     ```bash
     docker logout myregistry.example.com
     ```

   This command logs you out from the specified Docker registry.

3. **`docker logout --all`**: Log out from all registries.

   ```bash
   docker logout --all
   ```

   This command logs you out from all Docker registries that you have logged in to previously.

These commands are useful when working with private Docker registries that require authentication. The examples assume you are using a registry with the specified server address (replace `myregistry.example.com` with the actual address of your registry).

Remember to handle sensitive information like passwords and authentication tokens securely, especially when dealing with private registries. The `docker login` command securely stores credentials on your system for subsequent use.

## Dockerfile

### Basic Commands:

1. **`FROM`**: Specify the base image for the build.
   ```dockerfile
   FROM ubuntu:20.04
   ```

2. **`LABEL`**: Add metadata to an image.
   ```dockerfile
   LABEL maintainer="your-email@example.com"
   ```

3. **`RUN`**: Execute a command in the container during the build.
   ```dockerfile
   RUN apt-get update && apt-get install -y nginx
   ```

4. **`COPY`**: Copy files or directories from the build context to the image.
   ```dockerfile
   COPY ./app /usr/src/app
   ```

5. **`ADD`**: Similar to `COPY` but supports additional features like URL handling.
   ```dockerfile
   ADD http://example.com/file.tar.gz /tmp/
   ```

### Working Directory:

6. **`WORKDIR`**: Set the working directory for subsequent instructions.
   ```dockerfile
   WORKDIR /usr/src/app
   ```

### Environment Variables:

7. **`ENV`**: Set environment variables.
   ```dockerfile
   ENV NODE_ENV production
   ```

### Exposing Ports:

8. **`EXPOSE`**: Inform Docker that the container listens on the specified network ports.
   ```dockerfile
   EXPOSE 80/tcp
   ```

### Container User:

9. **`USER`**: Set the user or UID to use when running the image.
   ```dockerfile
   USER appuser
   ```

### Volume:

10. **`VOLUME`**: Create a mount point and/or mark it as holding externally mounted volumes from native host or other containers.
   ```dockerfile
   VOLUME /data
   ```

### Entry Point and Command:

11. **`CMD`**: Provide default arguments for the executable specified with `ENTRYPOINT`.
   ```dockerfile
   CMD ["nginx", "-g", "daemon off;"]
   ```

12. **`ENTRYPOINT`**: Configure a container that will run as an executable.
   ```dockerfile
   ENTRYPOINT ["nginx", "-g", "daemon off;"]
   ```

### Health Checks:

13. **`HEALTHCHECK`**: Check the status of the running container.
   ```dockerfile
   HEALTHCHECK --interval=5m --timeout=3s CMD curl -f http://localhost/ || exit 1
   ```

### Multi-Stage Builds:

14. **Multi-Stage `FROM`**: Use multiple `FROM` statements in a single Dockerfile.
   ```dockerfile
   FROM builder as intermediate
   RUN build-command

   FROM base
   COPY --from=intermediate /app/output /app/output
   ```

### Comments:

15. **`#`**: Add comments in the Dockerfile.
   ```dockerfile
   # This is a comment
   ```

These are just a few examples, and Dockerfile can be quite flexible. You can refer to the official Docker documentation for a more comprehensive list of commands and their usage: [Dockerfile Reference](https://docs.docker.com/engine/reference/builder/).

## Docker Swarm

Docker Swarm is a native clustering and orchestration solution for Docker, allowing you to create and manage a swarm of Docker nodes. It enables you to deploy and scale containers across multiple hosts, providing high availability and fault tolerance for your applications. In Docker Swarm, a group of Docker hosts (nodes) form a cluster and work together to manage containers.

Here are the key concepts in Docker Swarm:

1. **Node:** A Docker host that participates in the Swarm. Nodes can be either managers or workers.

2. **Manager Node:** Manages the Swarm and orchestrates the deployment of services. It also maintains the desired state of the swarm.

3. **Worker Node:** Executes tasks and runs containers.

4. **Service:** A definition of the tasks to execute on the manager or worker nodes. Services allow you to define the desired state of a containerized application.

Now, let's go through a basic example of setting up a Docker Swarm and deploying a service:

### Step 1: Initialize Swarm (On Manager Node)

On the manager node, initialize Docker Swarm:

```bash
docker swarm init --advertise-addr <MANAGER-IP>
```

This command will output a token that you can use to join other nodes to the swarm.

### Step 2: Join Worker Nodes to the Swarm

On each worker node, run the following command with the token obtained from the manager:

```bash
docker swarm join --token <TOKEN> <MANAGER-IP>:<MANAGER-PORT>
```

### Step 3: Deploy a Service

Now, you can deploy a service to the Swarm. For example, let's deploy a simple web service:

```bash
docker service create --replicas 3 -p 80:80 --name web nginx
```

This command creates a service named "web" with three replicas of the Nginx image, mapping port 80 on the host to port 80 on the service.

### Step 4: Scale the Service

You can scale the service by adjusting the number of replicas:

```bash
docker service scale web=5
```

This scales the "web" service to have five replicas.

### Step 5: Check Service Status

Check the status and details of the deployed service:

```bash
docker service ls
docker service ps web
```

### Step 6: Update the Service

You can update the service by changing its configuration. For example, update the Nginx version:

```bash
docker service update --image nginx:latest web
```

This updates the "web" service to use the latest version of the Nginx image.

### Step 7: Remove the Service and Leave Swarm

Remove the deployed service:

```bash
docker service rm web
```

To leave the Swarm on a node:

```bash
docker swarm leave
```

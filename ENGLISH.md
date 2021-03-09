# 🔷 Personal Docker Notes / Codes / Experience 
## General Commands:

`FROM`: Indicates from which base image the image to be created will be created. It is the only command that must be in the dockerfile file.

`RUN`: If there is a command that needs to be run in Shell while creating the image, it is written with RUN.

`WORKDIR`: Used to change directory. The only difference with the cd command is that the directory is created if it doesn't exist.

`COPY`: Copies file into image.

`ADD`: Adds a file in the image.

`ARG`: Allows to take arguments while the image is being built.

`EXPOSE`: It is specified with EXPOSE on which ports the containers to be created from this image will be broadcast.

`CMD`: When the container is created from this image, the command to be run by default is written.

`HEALTHCHECK`: With this command, it can be checked whether the container is running or not.

`ENV`: Enables the definition of environment variable.

`LABEL`: This command adds metadata inside the Dockerfile.

`ADD` and `COPY` Difference

`ADD` and `COPY` perform the same functions, but ADD also ensures that the file source is the URL.

If a .tar file is specified with `ADD`, this archive is copied to the image by `untar`.

`ENTRYPOINT` and `CMD` Difference

`ENTRYPOINT`, like `CMD`, cannot be changed after the image is created.

If both commands are written, what is written in the `CMD` command is added to `ENTRYPOINT` as parameters.

```
docker-compose used when developing, it is not used in production.
```

## Docker Commands:
### General
`docker version`: You can find out your version of docker with this command.

`docker info`: It allows you to see the containers and other system information on your system.

### Container
`docker ps`: Lists running containers.

`docker ps -a`: List all containers found in the system.

`docker container ls -a`: Functions the same as "docker ps -a".

`docker container ls -aq`: Lists the ID of all containers in the system.

`docker run --name hello-world hello-world`: Runs a container named hello-world.

`docker start hello-world`: Starts the container named hello-world.

`docker stop hello-world`: Stops the container named hello-world.

`docker logs hello-world`: Displays the logs of the container named hello-world.

`docker cp "container-id or container-name"`: path host_path: Copies file from container to host whose name or ID is given.

`docker run -d -p 8080: 80 "image-name"`: Can be run by giving the port number of the executed container. 8080 indicates the port of the host, 80 indicates the port of the container. Continuous operation is provided with "-d".

`docker run -dit "image-name" sh: "-dit"` command is a combination of -d -it -tty. Container runs in the background adding interactivity and so-called terminal connectivity.

`docker run -dit --net "network-name" "image-name" sh`: Creates a container with the created network.

`docker exec -it "container_id" sh`: It allows us to connect to the remote container with a shell connection.

`docker top "container name or id`: Indicates which processes are running in the container.

`docker run --rm -it hello-world sh`: Runs the container. `--rm` means delete after container is closed. `-it` is a combination of `--interactive` and `--tty`. Container makes interactive connections. With `sh` it also adds a terminal connection to the gasketinera on the remote machine. `--rm` only happens when the container is running interactively. With `-d` (detach), we can't say it should work in the background.

`docker stats "container name or id"`: Indicates how much resources the running container is using.

`docker attach "container-name or id"`: Used to connect to a container running in the background.

`docker run -d --memory = 100m "image-name"`: Defines the 100mb memory limit for the container to be created.

`docker run -d --cpus = "1.5" "image-name"`: It allows to use 1.5 of the processor cores in the system.

`docker run -d --cpuset-cpus = "1,4" "image-name"`: It enables the processor in the system to use processors 1 and 4.

`docker run --env deg1 = test "image-name"`: defines an environment variable named deg1.

`docker container rm "container name or id"`: Deletes the container whose name or ID is given.

`docker container rm -f "container name or id"`: Deletes the container whose name or ID is given even while it is running.

`docker container prune`: Deletes all non-working containers.

`docker system prune`: Cleans all unused containers, unused networks, unused images and build caches on the system.

`ce-name "sh`: Makes an interactive shell connection to the service created with Compose.

`docker-compose build`: if the image is created with build in yaml file, it saves the later changes in the image and makes the image with the new changes ready to be used

### Swarm
`docker swarm init`: swarm is activated on the machine where the command is run.

`docker swarm init --advertise-addr "ip-addr"`: Swarm is activated on the machine whose IP address is given.

`docker swarm join-token worker`: Brings the token needed to add a worker.

`docker swarm join-token manager`: Brings the token required to add a manager.

`docker node ls`: Find nodes in the cluster.

`docker service create --name "service-name" --replicas = 5 -p 8080: 80 "image-name"`: Creates the service whose name is service-name, which redirects port 8080 to port 80 of the service and has 5 replicas.

`docker service ps "service-name"`: Displays the tasks of the named service.

`docker service ls`: Lists running services.

`docker service inspect "service-name"`: Shows the details of the named service.

`docker service logs "service-name"`: Shows the logs of the named service.

`docker service rm "service-name"`: Deletes the named service. It deletes the service directly without verification, and should be careful when using it.

### Stack
`docker stack ls`: List the stacks.

`docker stack services "stack-name"`: Lists the services of the named stack.

`docker service ps "service-name"`: Lists the tasks of the named service.

`docker stack rm "stack-name"`: Deletes the named stack.

`docker stack deploy "stack-name"`: Restores the new stack whose name is written or updates the existing stack.

### Secret
Docker secret create creates a secret named `"secret-name"` file: `secret-name`.

`docker secret ls`: Lists the secrets in the system.

`docker secret inspect "secret-name"`: Gives details of the named secret.

`docker secret rm "secret-name"`: Deletes the named secret.

`echo "test" | docker secret create "secret-name"`: Creates a secret on the terminal.

`docker service update --secret-rm "secret-name" "service-name"`: Deletes the named secret in the named service.

`docker service update --secret-add "secret-name" "service-name"`: Adds the named secret to the named service.

### Logs
`docker logs "container name or id"`: Fetches logs after the container runs.

`docker logs -f "container name or id"`: Displays instant logs of the running container.

### Save and Load
`docker save "image-name" -o "image-name.tar"`: Converts the image to a tar archive.

`docker load -i "image-name.tar"`: converts tar archive to image.

### Docker Commit
`docker commit "container-id" "image-name"`: Creates a new image from changes in the container.

### Image
`docker image build -t "image-name"`: Performs image build operation after dockerfile script.

`docker image build -t "image-name" -f "dockerfile-name"`: Builds an image from a different Dockerfile.

`docker images`: Lists images on the system.

`docker image rm "image-name"`: Deletes the image.

`docker image prune -a`: Deletes all non-working images.

`docker history "image-name"`: Shows the history of the image.

### Volume
`docker volume create firstvolume`: creates a volume named firstvolume.

`Docker volume inspect firstvolume`: returns firstvolume details.

`docker volume ls`: Lists the volumes available in the system.

`docker volume rm "volume-name"`: Deletes the named volume.

`docker volume prune`: Deletes all volumes in the system.

### Network
`docker network create "name"`: Creates a network with the default network driver.

`docker network ls`: Lists Docker Network objects.

`docker network connect "network-name" "container name or id"`: It allows to connect the given container name or ID to the network created by the user. Network connection can only be done in the network created by the user.

`docker network disconnect "network-name" "container name or id"`: Disconnects the given container name or ID from the network created by the user.

`docker network rm "network-name"`: Allows network deletion.

### Compose
`docker-compose ps`: Lists running containers created with docker-compose.

`docker-compose ps -a`: List all containers created with docker-compose.

`docker-compose up`: Restores services. Does not revert to Shell.

`docker-compose down`: Stops and deletes services. If volume is defined in yaml file, it does not delete volumes. If an image is created from the yaml file with "build", the image is not deleted either.

`docker-compose up -d`: Enable services. It returns to Shell.

`docker-compose config`: lists the contents of the yaml file in reverse order.

`docker-compose images`: Lists from which images the created services were created.

`docker-compose logs`: Displays the logs of the services.

`docker-compose exec "service-name" sh`: Makes an interactive shell connection to the service created with Compose.

`docker-compose build`: if the image is created with build in yaml file, it saves the later changes in the image and makes the image with the new changes ready to be used

### Swarm
`docker swarm init`: swarm is activated on the machine where the command is run.

`docker swarm init --advertise-addr "ip-addr"`: Swarm is activated on the machine whose IP address is given.

`docker swarm join-token worker`: Brings the token needed to add a worker.

`docker swarm join-token manager`: Brings the token required to add a manager.

`docker node ls`: Find nodes in the cluster.

`docker service create --name "service-name" --replicas = 5 -p 8080: 80 "image-name"`: Creates the service whose name is service-name, which redirects port 8080 to port 80 of the service and has 5 replicas.

`docker service ps "service-name"`: Displays the tasks of the named service.

`docker service ls`: Lists running services.

`docker service inspect "service-name"`: Shows the details of the named service.

`docker service logs "service-name"`: Shows the logs of the named service.

`docker service rm "service-name"`: Deletes the named service. It deletes the service directly without verification, and should be careful when using it.

### Stack
`docker stack ls`: List the stacks.

`docker stack services "stack-name"`: Lists the services of the named stack.

`docker service ps "service-name"`: Lists the tasks of the named service.

`docker stack rm "stack-name"`: Deletes the named stack.

`docker stack deploy "stack-name"`: Restores the new stack whose name is written or updates the existing stack.

### Secret
`Docker secret create creates a secret named "secret-name" file`: secret-name.

`docker secret ls`: Lists the secrets in the system.

`docker secret inspect "secret-name"`: Gives details of the named secret.

`docker secret rm "secret-name"`: Deletes the named secret.

`echo "test" | docker secret create "secret-name"`: Creates a secret on the terminal.

`docker service update --secret-rm "secret-name" "service-name"`: Deletes the named secret in the named service.

`docker service update --secret-add "secret-name" "service-name"`: Adds the named secret to the named service.

### Logs
`docker logs "container name or id"`: Fetches logs after the container runs.

`docker logs -f "container name or id"`: Displays instant logs of the running container.

### Save and Load
`docker save "image-name" -o "image-name.tar"`: Converts the image to a tar archive.

`docker load -i "image-name.tar"`: converts tar archive to image.

### Docker Commit
`docker commit "container-id" "image-name"`: Creates a new image from changes in the container.

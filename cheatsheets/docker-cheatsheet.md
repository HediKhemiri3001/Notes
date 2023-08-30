# Docker

This cheatsheet provides commands and options often used when using docker.

Current completion status:

- [x] 25%
- [x] 50%
- [x] 75%
- [x] 100% (testing)

## Docker CLI

### Container

**Running** a container from image and mapping ports.

> `docker run -itd --name container_name -p  host:container image_name`

---

Checking **information** of a container

> `docker container inspect container_name`

---

Check **list** of all containers

> `docker container ps [-a]`

-a for listing all containers even those **not running**

---

**Copying** files between host and container

> `docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH
docker cp [OPTIONS] SRC_PATH CONTAINER:DEST_PATH `

First is from container to machine, **second** is from machine to container

---

**Execute a command** in the container

> `docker container exec container command`

---

**Start** an inactive container

> `docker container start -d container_id`

**Stop** a running container

> `docker container stop container_name`

**Kill** a running container

> `docker container kill container_name`

**Restart** a container

> `docker container restart container_name`

---

**Attach** to a container

> `docker container attach container_name`

---

**Rename** a container

> `docker container rename container_name container_new_name`

---

**Remove all inactive** containers

> `docker container prune `

---

**Remove** a container

> `docker container rm container_name`

---

**Top processes** of a container

> `docker container top container_name`

---

**Commit** a container, **creating an image**

> `docker container commit container -t resource:tag`

resource respresents image name, and tag version.

---

**Export** a container and its filesystem as tar

> `docker container export container_name`

---

### Images

**Listing** images

> `docker image ls`

---

**Pulling** an image from a registry

> `docker image pull image_name:tag`

eg. `docker image pull nginx:latest`

**Pushing** an image to registry

> `docker image push [registry.com]/image_name:tag`

---

**Importing** an image from a **tarball**

> `docker image import file|URL repo:tag`

\*This will import an image from a tar file and name it repo with tag tag.

**Saving** one or more images to a tar archive

> `docker image save image_1 image_2 `

**Load** an image from a tar archive

> `docker image load -i archive_name`

---

**History** of a docker images (**layers**)

> `docker image history image_name`

\*Layers are changes made to the container filesystem
Docker uses to make building more efficient, once you run a container based on an image, docker creates a new read and write layer on top of the base image, and as such if you commit a container that miniscule layer will be added on top of the image which is faster than rebuilding it completely, this is also true for removing a container, only that layer is removed and the base image is intact.

---

**Changing tag or name** of an image

> `docker image tag initial_image [registry/]new_image_name:new_tag`

---

**Inspecting** an image, e.g getting information such as env vars and other things

> `docker image inspect image`

---

**Removing** an image

> `docker image rm image`

**Removing all ununsed** images

> `docker image prune`

---

**Build** an image from a dockerfile

> `docker build [options] file_path`

\*This command can take alot of options allowing configuration management of result image.

---

## Dockerfile

- `FROM image_name:tag`: specifies the base image to use for the new image.
- `MAINTAINER author`: sets the author field of the image.
- `RUN command args`: executes a command and creates a new layer on top of the current image.

- `CMD ["command", "options", "arguments"]`: sets the default command to run when the container is launched.

- `LABEL`: adds metadata to the image.
- `EXPOSE port_number`: exposes a port for networking.
- `ENV VARIABLE_NAME variable_value`: sets an environment variable in the image.
- `ADD source_path_or_url destination_on_container`: copies a file, directory or remote file URL to the image.
- `COPY source_path destination_on_container`: copies files from the build context to the image.
- `ENTRYPOINT ["cmd","options","args"]`: specifies the command to run when the container is launched.
- `VOLUME /path/to/volume`: creates a mount point for storing data.
- `USER username[:group]`: sets the user or UID that will run the subsequent commands.
- `WORKDIR directory`: sets the working directory for subsequent commands, (as if you did cd to that directory).
- `ARG VAR_NAME=default_value`: defines a build-time argument to be passed to the Docker build command. this var can be accessed within the file using `${VAR_NAME}` and specified when building using `--build-arg MY_VAR=value`
- `ONBUILD DOCKERFILE_COMMAND `: specifies a command to be run when the image is used as the base for another image.
- `STOPSIGNAL <signalcode>`: sets the signal to be sent to the container when it is stopped.
- `HEALTHCHECK --interval=time --timeout=time CMD command_for_healthchecking`: sets a command to run to check the container health.
- `SHELL ["executable_path", "options"]`: sets the default shell used to run subsequent commands.

## Docker Compose

the `docker-compose.yaml` file represents a number of containers with their respective images and configuration.

here's an example:

```
version: '3'
services:
  nginx-1:
    image: nginx:latest
    container_name: nginx-1
    networks:
      my-network:
        ipv4_address: 172.25.0.2
    ports:
      - "8080:80"
    restart: always
  nginx-2:
    image: nginx:latest
    container_name: nginx-2
    networks:
      my-network:
        ipv4_address: 172.25.0.3
    ports:
      - "8081:80"
    restart: always
  redis:
    image: redis:latest
    container_name: redis
    networks:
      my-network:
        ipv4_address: 172.25.0.4
    environment:
      MYSQL_ROOT_PASSWORD: example
    volumes:
      - ./data:/var/lib/mysql
    restart: always

networks:
  my-network:
    ipam:
      config:
        - subnet: 172.25.0.0/16
```

---

To **validate** and **view** such a file we use :

> `docker-compose config`

---

To **run** a docker compose file we use:

> `docker-compose up [-d]`

-d to dettach

---

To **stop and remove** services started by a docker-compose file:

> `docker-compose down`

---

To **stop** services ran by a docker-compose file:

> `docker-compose stop`

---

To **start** services ran by a docker-compose file:

> `docker-compose start`

---

You can do the same operations with docker-compose, that you can do with docker.

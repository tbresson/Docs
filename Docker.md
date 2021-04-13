# Docker

## Display Docker version and info

* docker --version
* docker version
* docker info

## List Docker CLI commands

* docker
* docker container --help

## Docker search

* docker search some-repo                             # Search repositories * on Docker Hub via commandline

## Docker auth

* docker login                                        # Log in this CLI session using your Docker credentials

## Docker images

* docker image ls
* docker image ls -a                                  # List all images on this machine
* docker pull image-name                              # Pull image from Docker Hub
* docker image rm image-id                            # Remove specified image from this machine
* docker image rm $(docker image ls -a -q)            # Remove all images from this machine
* docker image prune                                  # Remove all images not in use
* docker images -f dangling=true                      # Remove dangling images

## Docker run (image)

* docker run hello-world
* docker run --name hello hello-world                 # Name the container "hello"
* docker run -p 4000:80 friendlyhello                 # Run "friendlyname" mapping port 4000 to 80
* docker run -d -p 4000:80 friendlyhello              # Same thing, but in detached mode
* docker run username/repository:tag                  # Run image from a registry

## Docker containers

* docker container ls                                 # List all running containers
* docker container ls -a                              # List all containers
* docker inspect hash-value                           # Inspect a container
* docker container stop hash-value                    # Gracefully stop the specified container
* docker container kill hash-value                    # Force shutdown of the specified container
* docker container rm                                 # Remove specified container from this machine
* docker container rm -v hash-value                   # Remove default volume along with the container
* docker container rm $(docker container ls -a -q)    # Remove all containers
* docker container prune                              # Remove all stopped containers

## Docker interactions/sessions

* docker run -it image                                # Start interactive session with the container
* CTRL+PQ                                             # Quit and leave session running
* docker attach hash                                  # Attach to a running container
* docker exec -it docker-id program-name              # Run a command or program inside a running container

## Docker utilities

* Docker logs container-id                            # Show all output from a containers creation

## Docker storage/volumes                             # Volumes are not removed when a container is removed

* docker run -d -v C:\Local:C:\Container image        # Mounts the containers dir to the local, e.g. for DB's
* docker volume ls                                    # Lists all volumes
* docker volume ls -f dangling=true                   # Find dangling (lost) volumes for existing containers (f=filter)
* docker volume rm $(docker volume ls -q)             # Remove volumes
* docker volume prune                                 # Remove all unused volumes

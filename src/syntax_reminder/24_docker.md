# Docker

- [Help](#help)
- [Exec](#exec)
- [Inspect](#inspect)
- [Restart](#restart)
- [Logs](#logs)
- [Containers](#containers)
- [Volumes](#volumes)
- [Images](#images)
  - [Image location](#image-location)
- [Networks](#networks)
- [Disk usage](#disk-usage)
- [Clean up](#clean-up)
- [Backups](#backups)
- [Docker compose](#docker-compose)
  - [Services](#services)
  - [Monitoring](#monitoring)
  - [Remove volume](#remove-volume)

## Help

``` bash
<docker_command> --help
```

## Exec

``` bash
docker exec -it <container_name> /bin/my_executable
docker exec -it <container_name> my_script.sh
```

## Inspect

``` bash
docker inspect <image_id>
docker inspect <container_id>
```

## Restart

``` bash
docker inspect <container_name> | grep -A 3 RestartPolicy # Check restart policy
docker update --restart=no <container_name> # Turn off restart
```

## Logs

``` bash
docker logs <container_id>
docker logs -n 10000 <container_id> # Show the last lines of the logs
docker logs --since=60m <container_id> # Show logs for last hour
docker logs --until=60s <container_id> # Show logs for next minute
```

## Containers

``` bash
docker create <image_name> # Create container from image
docker run <image_name> # Create and run container from image
docker start <container_name> # Start container
docker stop <container_name> # Stop container
docker restart <container_name> # Restart container
docker pause <container_name> # Pause container
docker unpause <container_name> # Resume container
docker ps # List running containers
docker ps --filter "status=exited" # List stopped containers
docker ps -a # List all containers
docker ps -sa # List size of all containers
docker container ls # List running containers
docker container ls -a # List all containers
docker rm <container_name> # Remove container
docker attach --sig-proxy=false <container_name> # Attach container; Ctrl+C won't kill process (if --sig-proxy is true (the default), CTRL+C sends a SIGINT to the container)
docker inspect $(docker ps -qa) |  jq -r 'map([.Name, .GraphDriver.Data.MergedDir]) | .[] | "\(.[0])\t\(.[1])"' #  Which container owns which overlay directory
docker inspect $(docker images) |  jq -r 'map([.Name, .GraphDriver.Data.MergedDir]) | .[] | "\(.[0])\t\(.[1])"' #  Which image owns which overlay directory
```

## Volumes

``` bash
docker volume create <volumne_name> # Create volume
docker volume rm <volumne_name> # Remove volume
docker volume inspect <volumne_name> # Inspect volume
docker volume ls # List all volumes
docker volume ls -f dangling=true # List dangling volumes
docker volume prune # Remove all unused volumes
```

## Images

``` bash
docker build -f <path_to_dockerfile> # Build image from dockerfile
docker build -t <my_image_tag> . # Build image and tag the resulting image
docker commit <container_name> <image_name> # Build image from running container
docker image pull <image_name> # Pull image from docker hub
docker image push <image_name> # Push image to docker hub
docker image ls # List images
docker image ls -a # List all images
docker images # List images
docker images -a # List all images
docker inspect --format='{{.Id}} {{.Parent}}' $(docker images --filter since=<image_id> -q) # Find the image id and parent id
docker rmi <image_id> # Remove image
docker rmi -f <image_id> # Force remove or remove container first
docker images -f dangling=true # List dangling images
docker rmi $(docker images -f dangling=true -q) # Remove dangling images
docker rmi <repo:tag> # Untags image
docker image prune # Remove all dangling images
docker image prune -a # Remove all dangling images not referenced by any container
```

### Image location

``` bash
cd /var/lib/docker/overlay2
du -h --summarize
```

## Networks

``` bash
docker network ls # List all networks
docker network create <network_name> # Create a user-defined bridge network
docker network rm <network_name> # Remove a user-defined bridge network
docker network connect <network_name> <container_name> # Connect container to network
docker network disconnect <network_name> <container_name> # Disconnect container from network
docker network inspect <network_name> # Inspect network
docker create --network <network_name> # Connect container to network
docker run --network <network_name> # Connect container to network
docker network connect <network_name> <container_name> # Connect a running container to an existing user-defined bridge
```

## Disk usage

``` bash
docker system df # Disk usage
docker system df --verbose # Disk usage
docker images # Show images
docker images -f dangling=true # List dangling images
docker volume ls # Show volumes
sudo du -d 1 -h # Disk usage of volume directory
```

## Clean up

``` bash
docker system prune # Clean up any images, containers, volumes, and networks that are dangling
docker builder prune # Remove build cache
docker container prune # Remove all stopped containers
docker image prune # Remove all dangling images
docker image prune -a # Remove all dangling images not referenced by any container
docker rmi $(docker images -f dangling=true -q) # Remove dangling images
docker volume prune # Remove all volumes not used by at least one container
docker network prune # Remove all networks not used by at least one container
```

## Backups

``` bash
docker save my_image > my_image.tar # Backup image
tar xvf my_image.tar | docker load # Load image from backup

docker export <container_name> > my_container.tar # Backup container
docker export [--output="my_image"] <container_name> # Backup container and specify output name
docker import < <image_name> # Import container from backup
```

## Docker compose

### Services

``` bash
docker-compose up # Start all containers, volumes, images, and networks in docker-compose.yml file
docker-compose up -d # Start container detached
docker-compose up -d --remove-orphans # Clean up orphan containers
docker-compose down # Stop and remove all containers, volumes, images, and networks in docker-compose.yml file
docker-compose down -v # Remove named volumes declared in the volumes section of the compose file and anonymous volumes attached to containers
docker-compose start # Start services
docker-compose stop # Stop services
docker-compose pause # Pause services
docker-compose unpause # Resume services
docker-compose restart # Restart services
docker-compose rm # Remove stopped containers
docker-compose pull # Pull images
docker-compose build # Rebuild a service if you change a service's dockerfile or the contents of its build directory
```

### Monitoring

``` bash
docker-compose ps # List containers deployed from a docker-compose.yml file
docker-compose images # List images in a docker-compose.yml file
docker-compose logs # View logs from running containers
docker-compose top # Display resource usage of containers
docker-compose config # Validate and view a docker-compose.yml file
```

### Remove volume

``` bash
docker-compose rm -f -v <volume_name> # Remove anonymous volume
docker-compose down -v # Remove all named volumes attached
```

# Docker install and config

## Docker version
- When talking about docker, it means we're mentioning to 2 differrent components of docker is: Client and Server (engine)
- To check version of both client and engine
```
docker version
```
After running above command, the result will be like this:
```
Client:
 Version:      18.03.1-ce
 API version:  1.37
 Go version:   go1.9.5
 Git commit:   9ee9f40
 Built:        Thu Apr 26 07:13:02 2018
 OS/Arch:      darwin/amd64
 Experimental: false
 Orchestrator: swarm

Server:
 Engine:
  Version:      18.03.1-ce
  API version:  1.37 (minimum version 1.12)
  Go version:   go1.9.5
  Git commit:   9ee9f40
  Built:        Thu Apr 26 07:22:38 2018
  OS/Arch:      linux/amd64
  Experimental: true
```

- To list detail info:
```
docker info
```

## Commandline old way and new way
- Old way
```
docker <command> <option>
```

- New way. Because of docker commands increase day by day, so they need to group into categories.
```
docker <management-command> <command> <option>
```

## What is a image, container?
- Image is bunch of binary files, libraries and source code.
- Container is a running instance of image.
- We can have many containers based on the same image.
- Images are stored in "registry". Docker's default image "registry" is DockerHub

## Container common commands
- Run a container of nginx web server
```
docker container run --publish 80:80 nginx
```

- To allow container runs in background, add --detach option to command
```
docker container run --publish 80:80 --detach nginx
```

- Everytime we run a new container, we'll get a new container ID

- Stop container
```
docker container stop <container-id/container-name>
```

- List running containers
```
docker container ls
```

- List all containers
```
docker container ls -a
```

- Create container with a name. If we do not specify name for container, docker will create a random name for us. That random name is from famous hackers or computer scientists.
```
docker container run --publish 80:80 --detach --name webhost nginx
```

- Logs
```
docker container logs <container-name>
```

- List processes are running containers
```
docker container top <container-name>
```

## Run mysql
```
docker container run --publish 3306:3306 --detach --name mysql -e MYSQL_RANDOM_ROOT_PASSWORD=yes mysql
```
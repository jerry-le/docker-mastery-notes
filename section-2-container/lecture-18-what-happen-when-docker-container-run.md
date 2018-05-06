# What happenned in background when we run `docker container run`?

- Looks for the local image in image cache, doesn't find anything
- Looks in remote image repository (default to Docker Hub)
- Downloads the latest version (nginx:latest by default)
- Creates new container based on that image and prepares to start
- Get a virtual IP on a private network inside docker engine 
- Open up port 80 on host and forwards to port 80 on container.
- Starts container by using the CMD in the image Dockerfile

[?] Where is the docker image cache?
```
~/Library/Containers/com.docker.docker/Data/
```

## What the container really is? It's just a process, not a mini VM
- A container is combined of processes. To find which processes are running a container:
```
docker top <container-name>
```
- For linux, the processes runs direct on the Linux kernel, so we can find the process by using: `ps aux`
- But for Mac, docker containers run on a tiny *Alpine Linux* running in a special *xhype* VM on MacOS. Thus, we cannot look for the process in `ps aux`. We need to access to that virtual machine (tiny Alpine Linux), then find the process. To do that, run this command:
```
screen ~/Library/Containers/com.docker.docker/Data/com.docker.driver.amd64-linux/tty
```
- Limited to what resources they can access
- Exit when process stop
# Dockerfile

> **Remember**: Each command will create a layer 

- `FROM` is required command in a Dockerfile
```
FROM debian:jessie
# all images must have a FROM
# usually from a minimal Linux distribution like debian or (even better) alpine
# if you truly want to start with an empty container, use FROM scratch
```

- `ENV` is variable environment. It is a key/value and it works everywhere, on every OS and config
```
ENV NGINX_VERSION 1.11.10
# optional environment variable that's used in later lines and set as envvar when container is running
```

- `RUN` is to execute command lines in the shell. Use `RUN` for install packages, unzip file or run the shell scripts.
    - To avoid too many layers are created when executing `RUN` commands, we need to group `RUN` commands into a single `RUN` command, thus docker will create only a single layer.
    ```
    RUN apt-get install package-1 \
    && apt-get update \
    && rm -rf ~/temp
    ```

    - About logging, we don't need to write logs to files, we only need to split logs to `stdin` and `stdout`, and Docker will do the rest for us.
    ```
    RUN ln -sf /dev/stdout /var/log/nginx/access.log \
        && ln -sf /dev/stderr /var/log/nginx/error.log
    # forward request and error logs to docker log collector
    ```

- `WORKDIR` is used to change the directory. We can use `RUN cd /path/to/workdir`, but don't do that. Whenever change the directory, let's use `WORKDIR`

- `COPY` is used to copy source code from local machine in to image working directory

- `EXPOSE` is used to expose ports on the docker virtual network
```
EXPOSE 80 443
# expose these ports on the docker virtual network
# you still need to use -p or -P to open/forward these ports on host
```

- `CMD` is required command. It runs everytime when we lauch new container from image, or start a stopped container. 
```
CMD ["nginx", "-g", "daemon off;"]
# required: run this command when container is launched
# only one CMD allowed, so if there are multiple, last one wins
```

## Build image

```
docker image build --tag <image-name> /path/to/folder-contain-dockerfile
```

- The order lines in the Dockerfile is very important. Because when we rebuild image, docker will re-run from the line has changes. So, it's so important to put the un-change things like OS, ENV, Packages into the first lines, and place often change things like the source code to nearly the end of Dockerfile.

> **CHANGE LESS at top, CHANGE MORE at bottom**
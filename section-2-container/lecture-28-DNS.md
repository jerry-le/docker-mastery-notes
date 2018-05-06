# DNS and how containers find each others.

- Forget IP: 
    - In the world of microservices, there are many container in a nerwork. These containers can be changing the IP when container down and up. So identify containers by IP is impossible. 
    - Don't use IP for talking to containers. It's too risk and easy to cause error
- What is the DNS?
    - DNS stands for Domain Name System
    - As we know, each web server has an IP address. To remember that IP address is quite not human readable. Instead of remembering '216.58.220.206', users only need to remember 'google.com'. 
    - DNS Server will map a domain name to its IP address
- Docker DNS: Docker Daemon has a built-in DNS server that containers use by default.

## Docker DNS
- We can use the container name as the DNS.
- Docker defaults the hostname is the container's name, but we can alse set aliases
- Assume, we have a network which has 2 containers: `my_nginx` and `new_nginx`. Docker DNS will default the hostname of `my_nginx` container is `my_nginx`, and the same with `new_nginx` container.
- So, we can ping each others by their container's name instead of their IP Address
```
docker container exec -it my_nginx ping new_nginx
```
- Remember, network driver "brigde" has no default DNS server built-in, so we can't use DNS for 2 contaniners in different brige networks. To link them, we need to specify `--link` when create container.
- In next sections, we'll learn about Docker Compose. Docker compose creates a virtual network our containers automatically.
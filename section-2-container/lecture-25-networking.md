# Networking in docker

## Check exposing port of a container
```
docker container port <container-name>
```

## Docker network default

- Each container connnected default to a private virtual network called "bridge"
    - bridge is the name of network driver too
    - if we don't specify network for container when create a new, docker will set to bridge by default
    - bridge network is used when our application run in standalone containers that need to communicate
    - to figure out more about Network Drivers: https://docs.docker.com/network/#network-drivers
- Each virtual network routes through NAT firewall on host IP (for connect to the Internet). NAT firewall is used to accepted only pre-defined routes from virtural network to host.
- All containers inside a virtual network can talk to each other without `-p`
- Best practice is to create a new virtual network for each app:
    - network "my_web_app" for php container
    - network "my_api" for web api

## Docker Networks Cont.
- A container can run on different networks or run on no network
- An network can manage multiple containers. Each container in that network must grap different ports.
- Containers in a same network can talk to each other without specify through `-p`

## Traffic flow and firewall

## CLI management Docker Network
- Show networks
```
docker network ls
```

- To inspect detail about a network
```
docker network inspect <network-name>
```

## Creating network
- We can create custom network. If not specify driver, then docker will create a new network with "bridge" drive by default.
```
docker network create my_network

docker network ls

NETWORK ID          NAME                DRIVER              SCOPE
742c160e6387        bridge              bridge              local
043ca3762b57        host                host                local
12480504df62        my_network          bridge              local
e909e8bffc9d        none                null                local
```

## Connect and disconnect a network to/from container
```
docker network connect NETWORK CONTAINER
```

```
docker network disconnect NETWORK CONTAINER
```

## Docker network - best practice for security
- Create your apps so frontend/backend sit on the same Docker network
- Their inter-communication never leaves host
- All externally exposed ports closed by default
- Must expose manually via `-p`, which is better default security
- Network will be much better with Swarm and Overlay network

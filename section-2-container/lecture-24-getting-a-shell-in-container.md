# Access into a container

- To get access into a container, we don't need to use ssh.
- Instead docker provides us some options:
```
docker exec -it <container-name> <program-inside-container>
```

Note: 
- `-t, -tty`: stand for terminal or teletypewriter
- `i` stands for interactive
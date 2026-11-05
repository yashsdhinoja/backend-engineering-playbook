# Basic Docker Commands

| Command | Work |
|---------|------|
| `docker pull ubuntu` | Download the Ubuntu image |
| `docker images` | Show all images |
| `docker run ubuntu` | Run an Ubuntu container (it exits quickly) |
| `docker run -it ubuntu bash` | Open an Ubuntu terminal |
| `exit` | Exit from the container |

## Practice

```bash
docker pull ubuntu
docker images
docker run ubuntu              # exits immediately, no foreground process
docker run -it ubuntu bash     # interactive terminal inside the container
exit
```

## Notes

- `-i` keeps input open and `-t` gives a terminal, so `-it` lets you interact with the container.
- `docker run ubuntu` exits quickly because Ubuntu has no long-running process by default.

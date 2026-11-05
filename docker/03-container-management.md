# Container Management Commands

| Command | Work |
|---------|------|
| `docker ps` | Show running containers |
| `docker ps -a` | Show all containers |
| `docker stop container_id` | Stop a container |
| `docker start container_id` | Start a stopped container |
| `docker rm container_id` | Delete a container |
| `docker exec -it container_id bash` | Go inside a running container |

## Practice

```bash
docker ps
docker ps -a
docker stop <container_id>
docker start <container_id>
docker exec -it <container_id> bash
docker stop <container_id>
docker rm <container_id>
```

## Notes

- Stop a container before removing it (or use `docker rm -f container_id`).
- You only need the first few characters of a container ID.

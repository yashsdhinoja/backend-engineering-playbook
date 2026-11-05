# How Docker Works

| Component | Definition | Work | Example |
|-----------|------------|------|---------|
| Docker CLI | Command line interface | Receives user commands | `docker run nginx` |
| Docker Engine | Main Docker system | Manages containers and images | Docker core service |
| Docker Daemon | Background process/service | Performs the actual Docker operations | Container create/run |
| Docker Image | Blueprint/template | Stores the files/dependencies needed to run an application | `nginx`, `ubuntu` |
| Docker Container | Running instance of an image | Runs the actual application | Running nginx server |
| Docker Hub | Online image repository | Images are downloaded/uploaded here | Docker image store |

## Flow

```
You (docker CLI) → Docker Daemon → pulls Image from Docker Hub → starts Container
```

## Key idea

An **image** is the blueprint. A **container** is a running instance of that image.

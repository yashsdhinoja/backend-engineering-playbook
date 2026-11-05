# 🐳 Docker Basics

Notes from my Docker learning and practice: what Docker is, how to install it on Windows and Mac, how it works, Docker Hub, and the terminal commands I practiced.

## Table of Contents

1. [What is Docker?](#1-what-is-docker)
2. [How Docker Works](#2-how-docker-works)
3. [Download and Install](#3-download-and-install)
4. [Docker Setup Check](#4-docker-setup-check)
5. [Docker Hub](#5-docker-hub)
6. [Terminal Commands](#6-terminal-commands)
7. [Practice Flow](#7-practice-flow)

---

## 1. What is Docker?

Docker is a tool that packages an application together with everything it needs to run (code, libraries, dependencies, settings) into a **container**. The container runs the same way on any machine, so "it works on my machine" stops being a problem.

**Why use it?**

- Same environment on every machine (dev, test, production)
- Lightweight and fast compared to virtual machines
- Easy to start, stop and delete applications
- Ready-made images (nginx, ubuntu, redis, etc.) can be downloaded in seconds

**Image vs Container**

| Term | Meaning |
|------|---------|
| Image | Blueprint / template (read-only) |
| Container | Running instance of an image |

---

## 2. How Docker Works

| Component | Definition | Work | Example |
|-----------|------------|------|---------|
| Docker CLI | Command line interface | Receives the commands the user types | `docker run nginx` |
| Docker Engine | Main Docker system | Manages containers and images | Docker core service |
| Docker Daemon | Background process/service | Performs the actual Docker operations | Container create/run |
| Docker Image | Blueprint/template | Stores the files/dependencies needed to run an application | `nginx`, `ubuntu` |
| Docker Container | Running instance of an image | Runs the actual application | Running nginx server |
| Docker Hub | Online image repository | Images are downloaded/uploaded here | Docker image store |

**Flow:**

```
You type a command  →  Docker CLI  →  Docker Daemon  →  pulls Image (from Docker Hub)  →  runs Container
```

---

## 3. Download and Install

Docker is installed on Windows and Mac through **Docker Desktop**. It includes Docker Engine, the CLI and a GUI to manage containers and images.

> Always download from the official site: https://www.docker.com/products/docker-desktop/
> Version-specific installers and changes are listed in the release notes: https://docs.docker.com/desktop/release-notes/

### 🪟 Windows

**Requirements**

- 64-bit Windows 10 or 11 (check the official docs for the exact supported builds)
- Hardware virtualization enabled in BIOS
- WSL 2 backend (installed automatically by Docker Desktop in most cases)

**Steps**

1. Download `Docker Desktop Installer.exe` from the official download page.
2. Double-click the installer and keep **Use WSL 2** selected.
3. Finish the install and restart the computer if asked.
4. Start Docker Desktop and wait until it shows **Docker is running**.

**Alternative (command line):**

```powershell
winget install Docker.DockerDesktop
```

Official guide: https://docs.docker.com/desktop/install/windows-install/

### 🍎 Mac

**Requirements**

- A supported macOS version (Docker Desktop supports the current and the two previous major macOS releases)
- Apple silicon (M1/M2/M3/M4) or Intel chip. Download the matching installer.

**Steps**

1. Download `Docker.dmg` for your chip (Apple silicon or Intel).
2. Open the `.dmg` and drag the Docker icon into **Applications**.
3. Open Docker from Applications and accept the subscription agreement.
4. Wait until Docker Desktop shows it is running.

**Optional (Apple silicon):** install Rosetta 2 for best compatibility:

```bash
softwareupdate --install-rosetta
```

Official guide: https://docs.docker.com/desktop/install/mac/

> **Licence note:** Docker Desktop is free for personal use, education and small businesses. Larger companies (more than 250 employees or more than $10 million USD annual revenue) need a paid subscription.

---

## 4. Docker Setup Check

After installation, open a terminal (PowerShell / Command Prompt on Windows, Terminal on Mac) and run:

```bash
docker --version
```

Shows the installed Docker version.

```bash
docker run hello-world
```

Downloads a tiny test image and runs it. If you see a "Hello from Docker!" message, your setup is working.

**Common problems**

| Problem | Fix |
|---------|-----|
| `Cannot connect to the Docker daemon` | Docker Desktop is not running. Start it and wait for the green/running status |
| Windows: WSL 2 error | Run `wsl --update` in PowerShell, then restart Docker Desktop |
| Windows: virtualization error | Enable virtualization (VT-x / SVM) in BIOS |
| Mac: app won't open | Check that your macOS version is supported and that you downloaded the right chip version |

---

## 5. Docker Hub

Docker Hub is the **online image repository** where Docker images are stored. When you run `docker pull ubuntu`, the image is downloaded from Docker Hub.

- Website: https://hub.docker.com
- Free account for pulling and pushing public images
- Official images available: `ubuntu`, `nginx`, `redis`, `node`, `python`, `mysql`, etc.

**Commands related to Docker Hub**

| Command | Work |
|---------|------|
| `docker login` | Log in to your Docker Hub account |
| `docker search nginx` | Search images on Docker Hub |
| `docker pull nginx` | Download an image from Docker Hub |
| `docker push username/image-name` | Upload your own image to Docker Hub |
| `docker logout` | Log out |

---

## 6. Terminal Commands

### Images and running containers

| Command | Work |
|---------|------|
| `docker pull ubuntu` | Download the Ubuntu image |
| `docker images` | Show all images |
| `docker run ubuntu` | Run an Ubuntu container (it exits quickly because there is no task to keep it running) |
| `docker run -it ubuntu bash` | Open an Ubuntu terminal inside the container |
| `exit` | Come out of the container |

### Managing containers

| Command | Work |
|---------|------|
| `docker ps` | Show running containers |
| `docker ps -a` | Show all containers |
| `docker stop container_id` | Stop a container |
| `docker start container_id` | Start a stopped container |
| `docker rm container_id` | Delete a container |
| `docker exec -it container_id bash` | Go inside a running container |

### Flag meanings

| Flag | Meaning |
|------|---------|
| `-i` | Interactive: keep input open |
| `-t` | Terminal: gives you a terminal |
| `-it` | Both together: interactive terminal |
| `-d` | Detached: run the container in the background |
| `-a` | All (with `docker ps`, includes stopped containers) |

> `container_id` is the ID shown in the first column of `docker ps`. A container name also works.

---

## 7. Practice Flow

A small hands-on exercise that uses all the commands above:

```bash
# 1. Download the image
docker pull ubuntu

# 2. Check it is downloaded
docker images

# 3. Open an Ubuntu terminal inside a container
docker run -it ubuntu bash

# 4. Try something inside, then leave
ls
exit

# 5. See the container you just used (it is stopped now)
docker ps -a

# 6. Start a container that keeps running in the background (-d = detached)
docker run -dit ubuntu bash
docker ps

# 7. Go inside the running container (use the ID from docker ps)
docker exec -it container_id bash
exit

# 8. Stop it, start it again, then stop and delete it
docker stop container_id
docker start container_id
docker stop container_id
docker rm container_id
```

> A container started with `docker run -it ubuntu bash` stops as soon as you `exit`. Starting it again with `docker start` will not keep it running unless it was created with `-d` (detached) as in step 6.

---

⬅️ Back to [Backend Engineering Playbook](../README.md)

# 🐳 Docker Basics – Complete Workflow Guide

A **step-by-step, beginner-friendly Docker guide** covering:

* Dockerfile creation
* Building images
* Pushing to Docker Hub
* Running containers
* Managing containers & images

This README contains **every step explained clearly** without skipping anything.

---

# 📦 STEP 1: Dockerfile

A **Dockerfile** contains instructions to build a Docker image.

### Example Dockerfile

```dockerfile
FROM python:3.10-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["python", "app.py"]
```

### Explanation

| Instruction                           | Meaning                                 |
| ------------------------------------- | --------------------------------------- |
| `FROM python:3.10-slim`               | Base image                              |
| `WORKDIR /app`                        | Sets working directory inside container |
| `COPY requirements.txt .`             | Copies requirements file                |
| `RUN pip install -r requirements.txt` | Installs dependencies                   |
| `COPY . .`                            | Copies all project files                |
| `CMD ["python", "app.py"]`            | Default command to run the app          |

---

# 🔨 STEP 2: docker build

Build a Docker image from the Dockerfile in the current directory.

* `-t` assigns a name (and optional tag) to the image.
* Here `myapp` is the image name.
* `latest` is the tag.
* If you don’t specify a tag, Docker automatically assigns it as `latest`.
* `.` means **Current directory**.
* When you run `docker build .`, Docker:

  * Looks for a Dockerfile in the current directory.
  * Sends all files in this directory to the Docker daemon.

```bash
docker build -t myapp:latest .
```

---

# 🚀 STEP 3: docker push

Before pushing, you must have a Docker account and must be logged in using:

```bash
docker login
```

Push the built image to a Docker registry (Docker Hub, ECR, etc.).

Image must be tagged with registry/repo name before pushing.

Here `username` is the owner of the Docker repository = `Sayandeep27`

Example:

```bash
docker push Sayandeep27/myapp:latest
```

---

# 🖼 STEP 4: docker images

List all Docker images available locally.

```bash
docker images
```

---

# ⬇️ STEP 5: docker pull

Pull an image from a Docker registry to local machine.

```bash
docker pull Sayandeep27/myapp:latest
```

---

# 📋 STEP 6: docker ps -a

List all containers:

* Running containers
* Stopped containers

```bash
docker ps -a
```

---

# ▶️ STEP 7: docker run

Create and start a container from an image.

### Important Flags

| Flag         | Meaning                                                                                                          |
| ------------ | ---------------------------------------------------------------------------------------------------------------- |
| `-d`         | Run in detached mode (background). Terminal is not blocked. Container keeps running even after closing terminal. |
| Without `-d` | Runs in foreground and shows logs directly.                                                                      |
| `-p`         | Map host port to container port                                                                                  |
| `--name`     | Assign a custom container name                                                                                   |

If you don’t give a container name, Docker creates random names like:

* `sleepy_hawking`
* `angry_morse`

### Example

```bash
docker run -d -p 8000:8000 --name myapp_container myapp:latest
```

* `myapp_container` → Container name
* `myapp` → Image name
* `latest` → Image tag

---

# ⏹ STEP 8: docker stop

Stop a running container gracefully.

```bash
docker stop myapp_container
```

---

# 🔄 STEP 9: docker start / docker restart

Start a stopped container:

```bash
docker start myapp_container
```

Restart a container (stop + start):

```bash
docker restart myapp_container
```

---

# ⏹ STEP 10: docker stop (again)

Stop the container before removing it.

```bash
docker stop myapp_container
```

---

# ❌ STEP 11: docker rm

Remove a stopped container.

```bash
docker rm myapp_container
```

---

# 🗑 STEP 12: docker rmi

Remove a Docker image from local system.

```bash
docker rmi myapp:latest
```

---

# ✅ Complete Workflow Summary

```text
Dockerfile → docker build → docker login → docker push
→ docker pull → docker run → docker stop/start/restart
→ docker rm → docker rmi
```

---

# 🎯 Final Notes

* Images are templates.
* Containers are running instances of images.
* You cannot remove an image if a container is using it.
* Always stop containers before removing them.

---

**Happy Dockering!** 🚀

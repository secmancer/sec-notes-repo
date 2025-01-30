### Introduction to Containerization
- **Purpose**: Package and run applications in isolated environments (containers).
- **Technologies**: Docker, Docker Compose, Linux Containers (LXC).
- **Advantages**:
  - **Lightweight**: Shares the host system's kernel.
  - **Portability**: Consistent across development, testing, and production.
  - **Scalability**: Run multiple containers on the same host.
- **Security**: Provides isolation but requires proper configuration to prevent vulnerabilities.



### Docker
- **Overview**: Open-source platform for automating application deployment in containers.
- **Key Features**:
  - Layered filesystem.
  - Resource isolation.
  - Portability and ease of use.
- **Installation**:
  ```bash
  # Preparation
  sudo apt update -y
  sudo apt install ca-certificates curl gnupg lsb-release -y
  sudo mkdir -m 0755 -p /etc/apt/keyrings
  curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
  echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

  # Install Docker Engine
  sudo apt update -y
  sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y

  # Add user to Docker group
  sudo usermod -aG docker $USER
  echo '[!] Log out and log back in for group changes to take effect.'

  # Test Docker installation
  docker run hello-world
  ```
- **Dockerfile**: Script to create Docker images.
  ```bash
  # Example Dockerfile
  FROM ubuntu:22.04
  RUN apt-get update && apt-get install -y apache2 openssh-server
  RUN useradd -m docker-user && echo "docker-user:password" | chpasswd
  RUN chown -R docker-user:docker-user /var/www/html
  EXPOSE 22 80
  CMD service ssh start && /usr/sbin/apache2ctl -D FOREGROUND
  ```
- **Building an Image**:
  ```bash
  docker build -t FS_docker .
  ```
- **Running a Container**:
  ```bash
  docker run -p 8022:22 -p 8080:80 -d FS_docker
  ```
- **Docker Management Commands**:
  | Command            | Description                          |
  |--------------------|--------------------------------------|
  | `docker ps`        | List running containers              |
  | `docker stop`      | Stop a running container             |
  | `docker start`     | Start a stopped container            |
  | `docker restart`   | Restart a container                  |
  | `docker rm`        | Remove a container                   |
  | `docker rmi`       | Remove a Docker image                |
  | `docker logs`      | View container logs                  |



### Linux Containers (LXC)
- **Overview**: Lightweight virtualization technology for running isolated Linux systems.
- **Key Features**:
  - Uses cgroups and namespaces for resource isolation.
  - Shares the host kernel for efficiency.
- **Installation**:
  ```bash
  sudo apt-get install lxc lxc-utils -y
  ```
- **Creating a Container**:
  ```bash
  sudo lxc-create -n linuxcontainer -t ubuntu
  ```
- **Managing LXC Containers**:
  | Command                          | Description                          |
  |----------------------------------|--------------------------------------|
  | `lxc-ls`                         | List all containers                  |
  | `lxc-stop -n <container>`        | Stop a container                     |
  | `lxc-start -n <container>`       | Start a container                    |
  | `lxc-restart -n <container>`     | Restart a container                  |
  | `lxc-attach -n <container>`      | Connect to a container               |
  | `lxc-config -n <container>`      | Manage container settings            |
- **Resource Limitation**:
  - Edit `/usr/share/lxc/config/<container>.conf`:
    ```bash
    lxc.cgroup.cpu.shares = 512
    lxc.cgroup.memory.limit_in_bytes = 512M
    ```
  - Restart LXC service:
    ```bash
    sudo systemctl restart lxc.service
    ```
- **Security Measures**:
  - Restrict access to containers.
  - Use cgroups to limit CPU and memory usage.
  - Isolate containers from the host system.



### Practical Applications
1. **Testing Environments**:
   - Create containers with specific software versions for testing.
   - Simulate vulnerable systems for penetration testing.
2. **Resource Management**:
   - Use cgroups to allocate CPU and memory resources.
   - Monitor container performance using `lxc-top`.
3. **Networking**:
   - Configure network settings for containers.
   - Use SSH for remote access to containers.
4. **Persistence**:
   - Save changes made to containers for reuse.
   - Use volumes to persist data outside containers.



### Exercises for Practice
1. Install LXC and create your first container.
2. Configure network settings for an LXC container.
3. Create a custom LXC image and launch a new container.
4. Configure resource limits (CPU, memory, disk space) for LXC containers.
5. Explore `lxc-*` commands for container management.
6. Create a container running a specific version of a web server (e.g., Apache, Nginx).
7. Configure SSH access to LXC containers and connect remotely.
8. Create a container with persistence to save changes.
9. Use LXC to test software in a controlled environment (e.g., vulnerable web apps).



### Summary
- **Docker**: Application-centric, portable, and easy to use.
- **LXC**: System-level, lightweight, and highly configurable.
- **Security**: Proper configuration is essential to prevent vulnerabilities.
- **Use Cases**: Testing, resource management, networking, and persistence.
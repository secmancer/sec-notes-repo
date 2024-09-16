- **Definition**: Packaging and running applications in isolated environments such as containers, virtual machines, or serverless environments.
- **Technologies**:
    - **Docker**
    - **Docker Compose**
    - **Linux Containers (LXC)**
- **Purpose**:
    - Efficiently manage, deploy, and scale applications.
    - Tailor applications based on user-specific configurations.
    - Ensure lightweight and isolated environments, ideal for running multiple applications simultaneously.

### Benefits of Containerization
- **Lightweight**: Containers use fewer resources than traditional virtual machines, allowing for greater scalability and performance.
- **Portability**: Applications can be easily moved between different environments (e.g., development, testing, production).
- **Isolation**: Containers provide separation between the host system and other containers, enhancing security.
- **Efficiency**: Running multiple applications simultaneously in isolated containers improves resource usage.


### Container Security
- **Isolation**: Containers are isolated from the host and other containers, offering an extra layer of protection against malicious activities.
- **Lightweight Nature**: Due to their design, containers are harder to compromise than traditional virtual machines.
- **Easy Configuration**: Containers can be easily configured to ensure secure application deployment.


### Security Considerations
- While containers provide many security benefits, methods for privilege escalation and container escape still exist, requiring careful security practices.

### Docker Overview
- **Definition**: Docker is an open-source platform used for automating the deployment of applications as containers.
- **Key Features**:
    - **Layered Filesystem**: Enhances flexibility and portability.
    - **Resource Isolation**: Ensures applications are securely separated.
    - **Tools**: Provides robust tools for creating, deploying, and managing applications, streamlining the containerization process.

### Installing Docker Engine on Ubuntu
- **Installation Script**:
    - Update system and install dependencies.
    - Add Docker’s GPG key and repository.
    - Install Docker components:
        - `docker-ce`
        - `docker-ce-cli`
        - `containerd.io`
        - Plugins for `buildx` and `docker-compose`
    - Add the user to the Docker group for permission management.
    - Test the installation using `docker run hello-world`.

### Docker Hub
- **Docker Hub**: A repository of pre-made Docker images, divided into public and private areas.
    - **Public Area**: Users can upload and share images, including official images from Docker and open-source projects.
    - **Private Area**: Images are accessible only to selected users, suitable for teams or companies.

### Creating Docker Images
- **Dockerfile**: Contains the instructions to create Docker containers.
    - Example: Creating a Dockerfile based on Ubuntu 22.04 with Apache and SSH.
        - **Base Image**: `ubuntu:22.04`
        - **Services**: Apache2 and OpenSSH server.
        - **User Setup**: Create a new user (`docker-user`) and configure access to Apache and SSH services.
        - **Expose Ports**: 22 (SSH), 80 (HTTP).
        - **CMD**: Start SSH and Apache services.

### Building and Running Docker Images
- **Building a Docker Image**:
    - Command: `docker build -t <tag> .`
    - Builds the image from the Dockerfile, tagging it for easier identification.
- **Running a Docker Container**:
    - Command: `docker run -p <host port>:<container port> -d <container name>`
    - Example: Running the `FS_docker` image with port mappings (8022 for SSH, 8080 for HTTP).

### Docker Management Commands
- **Common Commands**:
    - `docker ps`: List running containers.
    - `docker stop/start/restart <container>`: Control container execution.
    - `docker rm <container>`: Remove a container.
    - `docker rmi <image>`: Remove a Docker image.
    - `docker logs <container>`: View container logs.

![[Screenshot_20240912_142734.png]]
### Advanced Docker Considerations
- **Image Persistence**:
    - Any changes made to a running container are lost when it stops. For permanent changes, create a new image from a Dockerfile using `docker build`.
- **Container Orchestration**:
    - Tools like Docker Compose or Kubernetes help manage and scale containers in production environments. Docker Compose is useful for defining multi-container applications, while Kubernetes provides advanced orchestration features.


## Linux Containers
Linux Containers (LXC) offer a powerful and lightweight solution for running isolated Linux systems on a single host, leveraging features like cgroups and namespaces. LXC containers provide an isolated environment for applications, making them ideal for various tasks, such as testing software, configuring environments, and securely experimenting with exploits.


### Key Features of LXC:
1. **Lightweight Virtualization**: LXC uses the Linux kernel to provide isolation, resulting in minimal overhead compared to full virtualization technologies.
2. **Resource Isolation**: Using cgroups, LXC can limit CPU, memory, and other resources.
3. **Namespaces**: Provides process, network, and filesystem isolation, ensuring each container is self-contained.

### LXC vs Docker:
- **Approach**: LXC focuses on system-level containerization, creating isolated Linux systems. Docker focuses on application-level containerization.
- **Image Building**: LXC requires manual image building, while Docker uses a Dockerfile for more automated and portable image creation.
- **Portability**: Docker containers are more portable due to the abstraction layer provided by Docker. LXC containers are more tied to the host.
- **Ease of Use**: Docker has a more user-friendly interface, while LXC can be more technical to configure.
- **Security**: Docker incorporates more built-in security features, though LXC also provides robust isolation mechanisms.

![[Screenshot_20240912_142709.png]]
### Managing LXC Containers:
- **Creating a container**:
```
sudo lxc-create -n <container_name> -t <template>
```
- Example for Ubuntu:
```
sudo lxc-create -n linuxcontainer -t ubuntu
```

**Starting and stopping containers**:
- Start: `sudo lxc-start -n <container>`
- Stop: `sudo lxc-stop -n <container>`
- Restart: `sudo lxc-restart -n <container>`
**List containers**: `sudo lxc-ls`
**Attaching to a container**: `sudo lxc-attach -n <container>`

![[Screenshot_20240912_142722.png]]
### Securing LXC Containers:
LXC provides several security measures:
1. **Resource Limits**: Use cgroups to limit CPU, memory, or disk space usage.
```
Configuration:
sudo vim /usr/share/lxc/config/linuxcontainer.conf


Example configuration:
lxc.cgroup.cpu.shares = 512
lxc.cgroup.memory.limit_in_bytes = 512M

Restart LXC service to apply:
sudo systemctl restart lxc.service
```
2. **Namespace Isolation**: Ensure processes, networks, and filesystems are isolated from the host.
3. **SSH Access**: Secure access by limiting SSH or disabling it where unnecessary.

### Optional Exercises to Practice LXC:
1. Install LXC and create your first container.
2. Configure the network for your LXC container.
3. Create a custom LXC image and launch a new container.
4. Set resource limits for CPU, memory, and disk space.
5. Explore `lxc-*` commands for managing containers.
6. Set up a container with a specific version of a web server (e.g., Apache or Nginx).
7. Configure SSH access and connect remotely to your containers.
8. Create persistent containers that retain changes.
9. Use LXC to test software, such as vulnerable applications or malware, in a secure, isolated environment.
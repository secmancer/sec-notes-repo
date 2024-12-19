### Introduction
- **Containerization**: Containerization refers to the process of packaging and running applications in isolated environments, such as containers, virtual machines, or serverless platforms. This approach ensures that applications are isolated from each other and the host system, allowing for greater efficiency, security, and portability.
- **Technologies Enabling Containerization**: Several tools and technologies make containerization possible on Linux systems, including:
    - **Docker**: A popular platform that allows developers to easily create, deploy, and manage containers. Docker enables users to package applications and their dependencies into portable containers.
    - **Docker Compose**: A tool used alongside Docker to define and manage multi-container applications. It simplifies the orchestration of multiple containers, making it easier to deploy complex applications.
    - **Linux Containers (LXC)**: A set of tools that allows users to create lightweight virtual environments on Linux systems, similar to Docker but with a focus on providing more control over the containerized environment.
- **Advantages of Containers**:
    - **Lightweight**: Containers use fewer resources compared to traditional virtual machines (VMs), making them ideal for running multiple applications on the same system. They share the host system’s kernel and require less overhead.
    - **Portability**: Containers can be deployed on different systems, whether on a local machine, in a cloud environment, or across different operating systems, making them highly portable.
    - **Scalability**: Containers are easy to scale, allowing applications to be quickly replicated across different environments or systems based on demand.
    - **Efficiency**: Since containers are isolated, they ensure that applications run in the exact same environment, reducing compatibility issues between different environments.
- **Container Security**: Containers offer a secure environment by isolating applications from the host system and other containers. This isolation helps mitigate the risk of malicious activities affecting the host system or other applications. Some benefits of container security include:
    - **Isolation**: Containers ensure that each application runs in its own isolated environment, limiting the impact of potential vulnerabilities.
    - **Security Layers**: By using tools like Docker security scanning, users can identify vulnerabilities in container images before deployment.
    - **Lightweight and Harder to Compromise**: Because containers are lightweight, they typically have a smaller attack surface compared to traditional virtual machines, making them more secure and harder to compromise.
- **Escalation and Privilege Escaping**: While containers offer several security advantages, there are still methods for privilege escalation and escaping from containers. Vulnerabilities in container runtimes, misconfigurations, or insufficient isolation can allow attackers to break out of a container and gain access to the underlying host system. Therefore, it is important to implement strong security measures, such as:
    - Limiting container capabilities.
    - Using security-focused tools like SELinux, AppArmor, or seccomp to restrict access.
    - Keeping container images and host systems up to date with security patches.
    - Avoiding running containers with root privileges unless necessary.



### Dockers
- Docker is an open-source platform for automating the deployment of applications as self-contained units called containers. 
- It uses a layered filesystem and resource isolation features to provide flexibility and portability. 
- Additionally, it provides a robust set of tools for creating, deploying, and managing applications, 
- which helps streamline the containerization process.
- #### Install Docker-Engine
- Installing Docker is relatively straightforward. 
- We can use the following script to install it on a Ubuntu host.
```bash
#!/bin/bash

# Preparation
sudo apt update -y
sudo apt install ca-certificates curl gnupg lsb-release -y
sudo mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Install Docker Engine
sudo apt update -y
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y

# Add user htb-student to the Docker group
sudo usermod -aG docker htb-student
echo '[!] You need to log out and log back in for the group changes to take effect.'

# Test Docker installation
docker run hello-world
```
- The Docker engine and specific Docker images are needed to run a container. 
- These can be obtained from the [Docker Hub](https://hub.docker.com/), a repository of pre-made images, or created by the user. 
- The Docker Hub is a cloud-based registry for software repositories or a library for Docker images.
- It is divided into a `public` and a `private` area. 
- The public area allows users to upload and share images with the community.
- It also contains official images from the Docker development team and established open-source projects.
- Images uploaded to a private area of the registry are not publicly accessible. 
- They can be shared within a company or with teams and acquaintances.
- Creating a Docker image is done by creating a [Dockerfile](https://docs.docker.com/engine/reference/builder/), which contains all the instructions the Docker engine needs to create the container. 
- We can use Docker containers as our “file hosting” server when transferring specific files to our target systems. 
- Therefore, we must create a `Dockerfile` based on Ubuntu 22.04 with `Apache` and `SSH` server running. 
- With this, we can use `scp` to transfer files to the docker image, and Apache allows us to host files and use tools like `curl`, `wget`, and others on the target system to download the required files.
- Such a `Dockerfile` could look like the following.
- #### Dockerfile
```bash
# Use the latest Ubuntu 22.04 LTS as the base image
FROM ubuntu:22.04

# Update the package repository and install the required packages
RUN apt-get update && \
    apt-get install -y \
        apache2 \
        openssh-server \
        && \
    rm -rf /var/lib/apt/lists/*

# Create a new user called "student"
RUN useradd -m docker-user && \
    echo "docker-user:password" | chpasswd

# Give the htb-student user full access to the Apache and SSH services
RUN chown -R docker-user:docker-user /var/www/html && \
    chown -R docker-user:docker-user /var/run/apache2 && \
    chown -R docker-user:docker-user /var/log/apache2 && \
    chown -R docker-user:docker-user /var/lock/apache2 && \
    usermod -aG sudo docker-user && \
    echo "docker-user ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers

# Expose the required ports
EXPOSE 22 80

# Start the SSH and Apache services
CMD service ssh start && /usr/sbin/apache2ctl -D FOREGROUND
```
- After we have defined our Dockerfile, we need to convert it into an image. 
- With the `build` command, we take the directory with the Dockerfile, execute the steps from the `Dockerfile`, and store the image in our local Docker Engine.
- If one of the steps fails due to an error, the container creation will be aborted. 
- With the option `-t`, we give our container a tag, so it is easier to identify and work with later.
- #### Docker Build
```shell-session
secmancer@htb[/htb]$ docker build -t FS_docker .
```
- Once the Docker image has been created, it can be executed through the Docker engine, making it a very efficient and easy way to run a container. 
- It is similar to the virtual machine concept, based on images. 
- Still, these images are read-only templates and provide the file system necessary for runtime and all parameters.
- A container can be considered a running process of an image. 
- When a container is to be started on a system, a package with the respective image is first loaded if unavailable locally. 
- We can start the container by the following command [docker run](https://docs.docker.com/engine/reference/commandline/run/):
- #### Docker Run - Syntax
```shell-session
secmancer@htb[/htb]$ docker run -p <host port>:<docker port> -d <docker container name>
```
- #### Docker Run
```shell-session
secmancer@htb[/htb]$ docker run -p 8022:22 -p 8080:80 -d FS_docker
```
- In this case, we start a new container from the image `FS_docker` and map the host ports 8022 and 8080 to container ports 22 and 80, respectively. 
- The container runs in the background, allowing us to access the SSH and HTTP services inside the container using the specified host ports.
- #### Docker Management
- When managing Docker containers, Docker provides a comprehensive suite of tools that enable us to easily create, deploy, and manage containers. 
- With these powerful tools, we can list, start and stop containers and effectively manage them, ensuring seamless execution of applications. 
- Some of the most commonly used Docker management commands are shown below.
![[Screenshot_20241109_003111.png]]
- It is worth noting that these commands, used in Docker, can be combined with various options to provide additional functionality. 
- For example, we can specify which ports to expose, mount volumes, or set environment variables. 
- This allows us to customize our Docker containers to suit our needs and requirements. 
- When working with Docker images, it's important to note that any changes made to an existing image are not permanent.
- Instead, we need to create a new image that inherits from the original and includes the desired changes.
- This is done by creating a new Dockerfile that starts with the `FROM` statement, which specifies the base image, and then adds the necessary commands to make the desired changes. 
- Once the Dockerfile is created, we can use the `docker build` command to build the new image, tagging it with a unique name to help identify it. 
- This process ensures that the original image remains intact while allowing us to create a new image with the desired changes.
- It is important to note that Docker containers are designed to be immutable, meaning that any changes made to a container during runtime are lost when the container is stopped. 
- Therefore, it is recommended to use container orchestration tools such as Docker Compose or Kubernetes to manage and scale containers in a production environment.



### Linux Containers
- Linux Containers (`LXC`) is a virtualization technology that allows multiple isolated Linux systems to run on a single host. 
- It uses resource isolation features, such as `cgroups` and `namespaces`, to provide a lightweight virtualization solution. 
- LXC also provides a rich set of tools and APIs for managing and configuring containers, contributing to its popularity as a containerization technology. 
- By combining the advantages of LXC with the power of Docker, users can achieve a fully-fledged containerization experience in Linux systems.
- Both LXC and Docker are containerization technologies that allow for applications to be packaged and run in isolated environments. 
- However, there are some differences between the two that can be distinguished based on the following categories:
	- Approach
	- Image building
	- Portability
	- Easy of use
	- Security
- LXC is a lightweight virtualization technology that uses resource isolation features of the Linux kernel to provide an isolated environment for applications. 
- In LXC, images are manually built by creating a root filesystem and installing the necessary packages and configurations.
- Those containers are tied to the host system, may not be easily portable, and may require more technical expertise to configure and manage.
- LXC also provides some security features but may not be as robust as Docker.
- On the other hand, Docker is an application-centric platform that builds on top of LXC and provides a more user-friendly interface for containerization.
- Its images are built using a Dockerfile, which specifies the base image and the steps required to build the image. 
- Those images are designed to be portable so they can be easily moved from one environment to another.
- Docker provides a more user-friendly interface for containerization, with a rich set of tools and APIs for managing and configuring containers with a more secure environment for running applications.
- To install LXC on a Linux distribution, we can use the distribution's package manager. 
- For example, on Ubuntu, we can use the `apt` package manager to install LXC with the following command.
- #### Install LXC
```shell-session
secmancer@htb[/htb]$ sudo apt-get install lxc lxc-utils -y
```
- Once LXC is installed, we can start creating and managing containers on the Linux host. 
- It is worth noting that LXC requires the Linux kernel to support the necessary features for containerization. 
- Most modern Linux kernels have built-in support for containerization, but some older kernels may require additional configuration or patching to enable support for LXC.
- #### Creating an LXC Container
- To create a new LXC container, we can use the `lxc-create` command followed by the container's name and the template to use. 
- For example, to create a new Ubuntu container named `linuxcontainer`, we can use the following command:
```shell-session
secmancer@htb[/htb]$ sudo lxc-create -n linuxcontainer -t ubuntu
```
- #### Managing LXC Containers
- When working with LXC containers, several tasks are involved in managing them. 
- These tasks include creating new containers, configuring their settings, starting and stopping them as necessary, and monitoring their performance. 
- Fortunately, there are many command-line tools and configuration files available that can assist with these tasks. 
- These tools enable us to quickly and easily manage our containers, ensuring they are optimized for our specific needs and requirements. 
- By leveraging these tools effectively, we can ensure that our LXC containers run efficiently and effectively, allowing us to maximize our system's performance and capabilities.
![[Screenshot_20241109_003240.png]]
- As penetration testers, we may encounter situations where we must test software or systems with dependencies or configurations that are difficult to reproduce on our machines. 
- This is where Linux containers come in handy. 
- Since a Linux container is a lightweight, standalone executable package containing all the necessary dependencies and configuration files to run a specific software or system, it provides an isolated environment that can be run on any Linux machine, regardless of the host's configuration.
- Containers are useful, especially because they allow us to quickly spin up an isolated environment specific to our testing needs. 
- For example, we might need to test a web application requiring a specific database or web server version. 
- Rather than setting up these components on our machine, which can be time-consuming and error-prone, we can create a container that contains the exact configuration we need.
- We can also use them to test exploits or malware in a controlled environment where we create a container that simulates a vulnerable system or network and then use that container to safely test exploits without risking damaging our machines or networks. 
- However, it is important to configure LXC container security to prevent unauthorized access or malicious activities inside the container.
- This can be achieved by implementing several security measures, such as:
	- Restricting access to the container
	- Limiting resources
	- Isolating the container from the host
	- Enforcing mandatory access control
	- Keeping the container up to date
- LXC containers can be accessed using various methods, such as SSH or console. 
- It is recommended to restrict access to the container by disabling unnecessary services, using secure protocols, and enforcing strong authentication mechanisms.
- For example, we can disable SSH access to the container by removing the `openssh-server` package or by configuring SSH only to allow access from trusted IP addresses. 
- Those containers also share the same kernel as the host system, meaning they can access all the resources available on the system. 
- We can use resource limits or quotas to prevent containers from consuming excessive resources. 
- For example, we can use `cgroups` to limit the amount of CPU, memory, or disk space that a container can use.
- #### Securing LXC
- Let us limit the resources to the container. 
- In order to configure `cgroups` for LXC and limit the CPU and memory, a container can create a new configuration file in the `/usr/share/lxc/config/<container name>.conf` directory with the name of our container. 
- For example, to create a configuration file for a container named `linuxcontainer`, we can use the following command:
```shell-session
secmancer@htb[/htb]$ sudo vim /usr/share/lxc/config/linuxcontainer.conf
```
 - In this configuration file, we can add the following lines to limit the CPU and memory the container can use.
```txt
lxc.cgroup.cpu.shares = 512
lxc.cgroup.memory.limit_in_bytes = 512M
```
- When working with containers, it is important to understand the `lxc.cgroup.cpu.shares` parameter. 
- This parameter determines the CPU time a container can use in relation to the other containers on the system. 
- By default, this value is set to 1024, meaning the container can use up to its fair share of CPU time. 
- However, if we set this value to 512, for example, the container can only use half of the CPU time available on the system. 
- This can be a useful way to manage resources and ensure all containers have the necessary access to CPU time.
- One of the key parameters in controlling the resource allocation of a container is the `lxc.cgroup.memory.limit_in_bytes` parameter. 
- This parameter allows you to set the maximum amount of memory a container can use. 
- It's important to note that this value can be specified in a variety of units, including bytes, kilobytes (K), megabytes (M), gigabytes (G), or terabytes (T), allowing for a high degree of granularity in defining container resource limits. 
- After adding these two lines, we can save and close the file by typing:
	- `[Esc]`
	- `:`
	- `wq`
- To apply these changes, we must restart the LXC service.
```shell-session
secmancer@htb[/htb]$ sudo systemctl restart lxc.service
```
- LXC use `namespaces` to provide an isolated environment for processes, networks, and file systems from the host system. 
- Namespaces are a feature of the Linux kernel that allows for creating isolated environments by providing an abstraction of system resources.
- Namespaces are a crucial aspect of containerization as they provide a high degree of isolation for the container's processes, network interfaces, routing tables, and firewall rules. 
- Each container is allocated a unique process ID (`pid`) number space, isolated from the host system's process IDs. 
- This ensures that the container's processes cannot interfere with the host system's processes, enhancing system stability and reliability. 
- Additionally, each container has its own network interfaces (`net`), routing tables, and firewall rules, which are completely separate from the host system's network interfaces. 
- Any network-related activity within the container is cordoned off from the host system's network, providing an extra layer of network security.
- Moreover, containers come with their own root file system (`mnt`), which is entirely different from the host system's root file system.
- This separation between the two ensures that any changes or modifications made within the container's file system do not affect the host system's file system.
- However, it is important to remember that while namespaces provide a high level of isolation, they do not provide complete security. 
- Therefore, it is always advisable to implement additional security measures to further protect the container and the host system from potential security breaches.
- Here are 9 optional exercises to practice LXC:
![[Screenshot_20241109_003408.png]]

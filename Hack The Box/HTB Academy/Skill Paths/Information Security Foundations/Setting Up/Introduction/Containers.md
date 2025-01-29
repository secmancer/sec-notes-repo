### Definition and Characteristics
- **Containers**: Not virtual machines but isolated groups of processes running on a single host.
  - **Components**: Include complete application, configuration, and dependencies.
  - **Format**: Packaged in a precisely defined and reusable format.
  - **Operating System**: Do not contain their own OS or kernel, making them slimmer than VMs.
  - **Terminology**: Often referred to as application virtualization.



### Comparison with Virtual Machines
- **Virtual Machine (VM)**:
  - Contains applications and the complete operating system.
  - Requires a hypervisor (e.g., VMware ESXi) for virtualization.
  - Multiple VMs run in isolation on a physical server.
- **Container**:
  - Contains applications and only necessary OS components (e.g., libraries, binaries).
  - Uses the host OS with a container engine for virtualization.
  - Multiple containers run isolated on a single OS.



### Application Containers
- **Technical Basis**: Utilize Linux kernel functions for isolation.
  - **Isolation**: Applications run as isolated processes in different user accounts.
  - **Cooperation**: Applications can cooperate if running on the same system.
- **Container Daemon**: Example: Linux Container Daemon (LXD).
  - **LXC**: Linux Containers, a container-based virtualization technology.
    - Combines isolated namespaces and Linux kernel "cgroups".
    - Basis for Docker virtualization technology.
  - **LXD**: Used for configuring and controlling Linux OS containers via commands.
    - Suitable for automating mass container management in cloud computing and data centers.



### Container Images and Scalability
- **Container Image**: Basis of each container, can be pre-created or custom-made.
- **Scalability**: Containers are highly scalable, ideal for dynamic IT infrastructures.
  - **Orchestration Systems**: Tools like Apache Mesos and Google Kubernetes manage large container setups.
    - Distribute containers based on predefined rules and monitor them.



### Introduction to Docker
- **Docker**: Open-source software for isolating applications in containers.
  - **Simplifies Deployment**: Makes application data transport and installation easy.
  - **Resource Separation**: Ensures strict separation of computer resources.
  - **Docker Images**: Store programs with dependencies, forming the basis for virtualized containers.
    - **Portability**: Applications can run on almost any OS, making them portable and easy to scale.
- **Docker Engine**: Main component providing the interface between host resources and running containers.
  - **Compatibility**: Works on Linux, Windows (via VMware or Hyper-V), and Mac OS.
- #### Docker Installation
	- **Linux**:
  ```bash
  sudo apt update -y
  sudo apt install docker.io -y
  ```
	- **Windows**:
  ```powershell
  IEX((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))
  choco upgrade chocolatey
  choco install docker-desktop
  ```



### Introduction to Vagrant
- **Vagrant**: Tool for creating, configuring, and managing VMs or VM environments.
  - **Vagrantfile**: Describes VMs in code, which can include additional code files.
  - **Vagrant CLI**: Processes the code to create, provision, and start VMs.
  - **Providers**: Out-of-the-box support for VMware and Docker.
  - **Destruction**: VMs can be easily destroyed when no longer needed.



### Vagrant Installation
- **Linux**:
  ```bash
  sudo apt update -y
  sudo apt install virtualbox virtualbox-dkms vagrant
  ```
- **Windows**:
  ```powershell
  IEX((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))
  choco upgrade chocolatey
  cinst virtualbox cyg-get vagrant
  ```



#### Practical Recommendations
- **Experimentation**: Play around with different containers to understand their workings.
- **Documentation**: Read through documentation to grasp dependencies, advantages, and disadvantages.
### Basic Ideas
- Container: isolated group of processes running on a host, often corresponding to a complete application, along with its related configuration and dependencies.
- Unlike a usual VM, containers don't contain an OS or kernel. Therefore, they're also referred to as application virtualization in this context.
- Due to this, they are much more slim than more traditional VMs.
- Significant issue that we often find when the rollout of new applications or release of applications is that it depends on a certain environment being present.
	- A specific application needs specific local settings and function libraries, which may be different from development to production environments.
	- So, applications may end up behaving differently between the two.
![[Screenshot_20241107_150002.png]]
- While application containers are supposed to be based on features provided by Linux, the kernel instead chooses to isolate these applications from each other, and they achieve this by running them in different processes in different user accounts. 
- Overall though, they all belong to the same Linux environment in the end.
- Containers on the same system use a container daemon like `Linux Container Daemon` (`LXD`), which is similar to `Linux Containers` (`LXC`). LXC provides container-based virtualization at the OS level by isolating namespaces and utilizing Linux kernel "cgroups." 
- Historically, LXC was foundational to Docker.
- LXD enables the configuration and control of Linux OS containers through commands, making it suitable for automating mass container management, especially in cloud computing and data centers.
- Containers are highly scalable, supporting dynamic IT infrastructure needs. They are based on file system images, which can be pre-created or custom-made, allowing flexible resource allocation for application provisioning.
- Tools like `Apache Mesos` and `Google Kubernetes` manage large container setups by distributing containers across hardware, enforcing predefined rules, and monitoring operations.


### Docker
- [Docker](https://www.docker.com/get-started) is one of these container engines, available on Windows, Mac, and Linux operating systems.
- It's designed to isolate applications in containers to simplify the deployment of applications.
- This way, the application data stored in the containers can be transported and installed easily.
- We can also ensure that computer resources are strictly separated from each other. 
- Docker stores these apps/their dependencies together into images, which are the basis for these virtualized containers to run on almost any operating system, allowing for more portable and uncomplicated applications.
- Like mentioned above, the main component for this is [Docker Engine](https://docs.docker.com/engine/), which provides the interface between host resources and running containers. 
- Machines with Docker Engine install are able to run Docker containers.

### Docker Installation
```shell-session
secmancer@htb[/htb]$ sudo apt update -y 
secmancer@htb[/htb]$ sudo apt install docker.io -y
```
```powershell-session
C:\> IEX((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))
C:\> choco upgrade chocolatey
C:\> choco install docker-desktop
```

### Vagrant
- [Vagrant](https://www.vagrantup.com/) : tool to create, configure and manage virtual machines or virtual machine environments. 
- These VMs are not created and configured manually but rather are described in code, that in turn, is stored in a `Vagrantfile`. 
- To better structure the program code, the Vagrant file can include additional code files. 
- The code can then be processed using the Vagrant CLI. In this way, we can create, provision, and start our own VMs. 
- Moreover, if the VMs are no longer needed, they can be destroyed just as quickly and easily. 
- Out of the box, Vagrant offers providers for VMware and Docker.

### Vagrant Installation
```shell-session
secmancer@htb[/htb]$ sudo apt update -y 
secmancer@htb[/htb]$ sudo apt install virtualbox virtualbox-dkms vagrant
```
```powershell-session
C:\> IEX((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))
C:\> choco upgrade chocolatey
C:\> cinst virtualbox cyg-get vagrant
```
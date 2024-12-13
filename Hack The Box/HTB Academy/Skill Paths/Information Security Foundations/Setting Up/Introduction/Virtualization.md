### Debrief
- Virtualization abstracts physical computing resources—such as hardware, software, storage, and network components—making them available in a virtualized manner.
- **Key Benefits of Virtualization**:
    - Provides an abstraction layer between physical resources and virtual components.
    - Enhances flexibility and efficient resource utilization, especially important in cloud services.
- **Types of Virtualization**:
    - **Hardware Virtualization**: Involves the use of hypervisor software to abstract physical hardware and create virtual machines (VMs).
    - **Application Virtualization**: Virtualizing individual applications, allowing them to run independently of the underlying operating system.
    - **Storage Virtualization**: Combines physical storage into a single logical pool to improve storage management.
    - **Data Virtualization**: Provides access to data without the need to replicate or move it physically.
    - **Network Virtualization**: Combines physical network resources into a single, manageable pool.
- A VM acts like a physical computer, running an operating system and hardware on top of a host system managed by hypervisors.


###  Virtual Machines
- `Virtual machine (VM)`: virtual operating system that runs on a host system (an actual physical computer system). 
- Several VMs isolated from each other can be operated in parallel. 
- The physical hardware resources of the host system are allocated via `hypervisors`.
- This is a sealed-off, virtualized environment, where several guest systems can be operated, independent of the operating system, in parallel, on one physical computer.
- They can act independently of each other and do not influence each other. as the hypervisor manages the hardware resources, and from the virtual machine's point of view, allocated computing power, RAM, hard disk capacity, and network connections are exclusively available.
- From the application perspective, an operating system installed within the VM behaves as if installed directly on the hardware.
- It is not apparent to the applications or the operating system that they are running in a virtual environment. 
- Virtualization is usually associated with performance losses for the VM because the intermediate virtualization layer itself requires resources. 
- VMs offer numerous advantages over running an operating system or application directly on a physical system.
![[Screenshot_20241107_145756.png]]


### VMware
- VMware offers virtualization software, with **VMware Workstation Pro** and **VMware Workstation Player** being the most notable.
- **Workstation Pro vs. Workstation Player**:
    - **Workstation Pro**: Allows running multiple VMs simultaneously.
    - **Workstation Player**: Can only run one VM at a time.
- **VMware Workstation Pro 17**:
    - Installation files for Windows and Linux can be downloaded [here](https://support.broadcom.com/group/ecx/productfiles?subFamily=VMware%20Workstation%20Pro&displayGroup=VMware%20Workstation%20Pro%2017.0%20for%20Personal%20Use%20(Windows)&release=17.5.2&os=&servicePk=520448&language=EN).
    - Requires registration of a Broadcom account.
- Since Windows users are more familiar with VMware, the instructions will focus on installing VMware Workstation Pro on a Windows operating system.
- #### Installation on Windows
	- **Installation Process**:
	    1. Download the VMware Workstation Pro installation file and run it.
	    2. Choose additional features if necessary during the setup.
	    3. Complete the installation and restart the operating system.
	- **Post-Installation**:
	    - After restarting, an icon for VMware Workstation Pro will appear on the desktop.
	    - **VMware Workstation Player** interface will look like this, offering options to create a new VM or import an existing one.
	- **VM Format: Open Virtualization Format (OVF)**:
	    - VMs are deployed in OVF format, which is a standard for packaging and distributing virtual appliances or virtual machines.
	    - OVF is compatible with multiple platforms like VMware, VirtualBox, XenServer, Oracle VM, and more.
	    - More information about OVF can be found [here](https://en.wikipedia.org/wiki/Open_Virtualization_Format).
- #### Installation on Linux
	- Here, it works differently than Windows.
	- Once downloaded, we can run the installation within the Linux terminal.
```shell-session
username@Linux:~$ sudo apt install build-essential -y
username@Linux:~$ sudo bash ~/Downloads/VMware*.bundle

[sudo] password for user: **************

Extracting VMware Installer...done.
Installing VMware Installer 3.0.0
Copying files...
...SNIP...
Configuring...
Installation was successful.
```


### VirtualBox
- **VirtualBox** is a free alternative to VMware Workstation.
- It uses emulated hard disk container files called Virtual Disk Images (`VDI`).
- VirtualBox supports other hard disk formats like VMware's `.vmdk`.
- It also supports the `Virtual Hard Disk` format (`.vhd`), and more.
- These formats can be converted using the `VBoxManager` command-line tool.
- VirtualBox allows encrypting VMs, which is highly recommended for security.
- Encryption should be applied once the VM is configured and ready for use.
- VirtualBox can be installed via command line or downloaded and manually installed from the [official website](https://www.virtualbox.org/wiki/Downloads).
- #### Installation
```shell-session
secmancer@htb[/htb]$ sudo apt install virtualbox virtualbox-ext-pack -y
```

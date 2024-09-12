**Containers vs. Virtual Machines**
- **Containers** are isolated groups of processes running on a host system, packaged with the application, its configuration, and dependencies.
- Unlike VMs, containers do not include their own OS kernel, making them slimmer and more efficient.
- **Key Differences:**
    - VMs contain the full OS, while containers include only necessary OS components (libraries and binaries).
    - VMs are virtualized using hypervisors, while containers use the OS's container engine for virtualization.

**Linux Container Technology**
- **LXC (Linux Containers):** Combines isolated namespaces and "cgroups" in the Linux kernel for isolated environments.
- **LXD:** A container daemon similar to LXC, used for mass container management and suitable for cloud computing.
- Containers are scalable and can be managed using orchestration systems like **Kubernetes** or **Apache Mesos**, which distribute containers across hardware.

**Docker Overview**
- Docker is open-source software that isolates applications in containers, simplifying deployment and portability.
- **Docker Engine** is the core component, providing the interface between host resources and containers.
- Containers make applications portable across environments, allowing easy scaling of services like **SaaS clusters**.
- Docker works on **Linux**, but with VMware or Hyper-V, it also functions on **Windows** and **macOS**.

**Docker Installation**
- **Linux:**
```

```
- **Windows (with Chocolatey)**:
```

```

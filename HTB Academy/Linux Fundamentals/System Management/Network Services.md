### Network Services in Linux

#### Importance

Working with network services in Linux is crucial for:

- Communicating with other computers over the network
- Connecting and transferring files
- Analyzing network traffic
- Configuring services to identify vulnerabilities in penetration tests

#### SSH (Secure Shell)

- **Purpose**: Secure transmission of data and commands.
- **Common Server**: OpenSSH (free and open-source).
- **Install**: `sudo apt install openssh-server -y`
- **Check Status**: `systemctl status ssh`
- **Login Example**: ssh cry0l1t3@10.129.17.122
- **Configuration**: Edit `/etc/ssh/sshd_config` for settings like concurrent connections, login methods, and host key checking.

#### NFS (Network File System)

- **Purpose**: Manage and store files on remote systems as if local.
- **Install**: `sudo apt install nfs-kernel-server -y`
- **Check Status**: `systemctl status nfs-kernel-server`
- **Configuration**: Edit `/etc/exports` for shared directories and access rights.
- **Create Share Example**:
	- mkdir nfs_sharing
	- echo '/home/cry0l1t3/nfs_sharing hostname(rw,sync,no_root_squash)' >> /etc/exports
- **Mount Share Example**:
	- mkdir ~/target_nfs
	- mount 10.129.12.17:/home/john/dev_scripts ~/target_nfs

#### Web Server

- **Purpose**: Host and manage web applications.
- **Popular Servers**: Apache, Nginx, Lighttpd, Caddy.
- **Install Apache**: `sudo apt install apache2 -y`
- **Configuration**: Edit `/etc/apache2/apache2.conf` for directory access and settings.
- **Python Web Server**:
    - **Install Python**: `sudo apt install python3 -y`
    - **Start Server**: python3 -m http.server
	- **Custom Directory**: python3 -m http.server --directory /home/cry0l1t3/target_files
	- **Custom Port**: python3 -m http.server 443

#### VPN (Virtual Private Network)

- **Purpose**: Securely connect to another network via an encrypted tunnel.
- **Popular Servers**: OpenVPN, L2TP/IPsec, PPTP, SSTP, SoftEther.
- **Install OpenVPN**: `sudo apt install openvpn -y`
- **Configuration**: Edit `/etc/openvpn/server.conf`
- **Connect Example**: sudo openvpn --config internal.ovpn

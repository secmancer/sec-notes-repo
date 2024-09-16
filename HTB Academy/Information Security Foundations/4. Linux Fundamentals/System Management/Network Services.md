**Importance of Network Services in Linux:**
- Essential for network communication, file transfers, traffic analysis, and vulnerability assessment.
- Knowledge of network services helps in configuring and securing services and understanding network security implications.

**Key Network Services:**
#### SSH (Secure Shell)
- **Purpose:** Secure data and command transmission over a network.
- **Commonly Used Server:** OpenSSH.
- **Installation:**
```
sudo apt install openssh-server -y
```
- **Check Status:**
```
systemctl status ssh
```
- **Connect Remotely:**
```
ssh username@host_ip
```
- **Configuration File:** `/etc/ssh/sshd_config`
	- **Usage:** Adjust connection limits, authentication methods, etc.

#### NFS (Network File System)
- **Purpose:** Manage and store files on remote systems as if local.
- **Installation:**
```
sudo apt install nfs-kernel-server -y
```
- **Check Status:**
```
systemctl status nfs-kernel-server
```
**Configuration File:** `/etc/exports`
- **Access Rights:**
    - `rw`: Read and write access
    - `ro`: Read-only access
    - `no_root_squash`: Root access on the client is not restricted
    - `root_squash`: Root access is restricted
    - `sync`/`async`: Data transfer synchronization settings
- **Create Share:**
```
mkdir nfs_sharing
echo '/home/username/nfs_sharing hostname(rw,sync,no_root_squash)' >> /etc/exports
```
- **Mount NFS Share:**
```
mkdir ~/target_nfs
mount 10.129.12.17:/home/username/dev_scripts ~/target_nfs
```

#### Web Server
- **Purpose:** Serve data and applications over the Internet.
- **Popular Servers:** Apache, Nginx, Lighttpd, Caddy.
- **Apache Installation:**
```
sudo apt install apache2 -y
```
**Configuration File:** `/etc/apache2/apache2.conf`
- **Example Configuration:**
```
<Directory /var/www/html>
    Options Indexes FollowSymLinks
    AllowOverride All
    Require all granted
</Directory>
```


**Python Web Server:**
- **Install Python3:**
```
sudo apt install python3 -y
```
- **Start Server:**
```
python3 -m http.server
```
- **Specify Directory:**
```
python3 -m http.server --directory /path/to/folder
```
- **Change Port:**
```
python3 -m http.server 443
```


#### VPN (Virtual Private Network)
- **Purpose:** Securely connect to another network, encrypt data, and anonymize traffic.
- **Popular VPN Servers:** OpenVPN, L2TP/IPsec, PPTP, SSTP, SoftEther.
- **OpenVPN Installation:**
```
sudo apt install openvpn -y
```
- **Configuration File:** `/etc/openvpn/server.conf`
- **Connect to VPN:**
```
sudo openvpn --config /path/to/config.ovpn
```
- **Usage in Penetration Testing:** Connect to internal networks remotely for vulnerability assessment.
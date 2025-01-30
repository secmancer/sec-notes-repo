### Network Services Notes
- #### Importance of Network Services in Linux
	- **Essential for Remote Operations**: Network services enable tasks like remote connections, file transfers, and network traffic analysis.
	- **Security Implications**: Understanding these services helps identify vulnerabilities during penetration testing.
	- **Example Scenario**: A user connecting via unencrypted FTP exposes credentials in plain text, highlighting the need for secure protocols.
- #### Key Network Services
	1. **SSH (Secure Shell)**
	   - **Purpose**: Secure data and command transmission over a network.
	   - **Common Implementation**: OpenSSH.
	   - **Installation**:
     ```bash
     sudo apt install openssh-server -y
     ```
   - **Check Status**:
     ```bash
     systemctl status ssh
     ```
   - **Connecting via SSH**:
     ```bash
     ssh username@host_ip
     ```
   - **Configuration**: Edit `/etc/ssh/sshd_config` for settings like concurrent connections, authentication methods, etc.
2. **NFS (Network File System)**
   - **Purpose**: Share and manage files across networks as if they were local.
   - **Installation**:
     ```bash
     sudo apt install nfs-kernel-server -y
     ```
   - **Check Status**:
     ```bash
     systemctl status nfs-kernel-server
     ```
   - **Configuration**: Edit `/etc/exports` to specify shared directories and access rights.
     - **Permissions**:
       - `rw`: Read and write.
       - `ro`: Read-only.
       - `no_root_squash`: Root access on client.
       - `root_squash`: Restrict root access.
       - `sync`: Synchronous data transfer.
       - `async`: Asynchronous data transfer.
   - **Mounting NFS Share**:
     ```bash
     mkdir ~/target_nfs
     mount host_ip:/shared_directory ~/target_nfs
     ```
3. **Web Servers**
   - **Purpose**: Deliver data and applications over the internet using HTTP/HTTPS.
   - **Common Servers**: Apache, Nginx, Lighttpd, Caddy.
   - **Apache Installation**:
     ```bash
     sudo apt install apache2 -y
     ```
   - **Configuration**: Edit `/etc/apache2/apache2.conf` for global settings.
     - **Directory Access Example**:
       ```apache
       <Directory /var/www/html>
           Options Indexes FollowSymLinks
           AllowOverride All
           Require all granted
       </Directory>
       ```
   - **Python Web Server**:
     - **Start Server**:
       ```bash
       python3 -m http.server
       ```
     - **Specify Directory**:
       ```bash
       python3 -m http.server --directory /path/to/folder
       ```
     - **Custom Port**:
       ```bash
       python3 -m http.server 443
       ```
4. **VPN (Virtual Private Network)**
   - **Purpose**: Create a secure, encrypted tunnel for remote network access.
   - **Common Solutions**: OpenVPN, L2TP/IPsec, PPTP, SSTP, SoftEther.
   - **OpenVPN Installation**:
     ```bash
     sudo apt install openvpn -y
     ```
   - **Configuration**: Edit `/etc/openvpn/server.conf` for encryption, tunneling, etc.
   - **Connecting to VPN**:
     ```bash
     sudo openvpn --config internal.ovpn
     ```



### Summary
- **SSH**: Secure remote access and file transfer.
- **NFS**: Efficient file sharing across networks.
- **Web Servers**: Host and manage web applications.
- **VPN**: Secure remote access to internal networks.
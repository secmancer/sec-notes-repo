### **Overview**
- A Virtual Private Server (VPS) is crucial for penetration testing. It provides a centralized, remotely accessible platform for managing resources, tools, and services. This example uses **Vultr** as the VPS provider, but the setup steps are similar across providers.



### **Steps for VPS Setup**
- #### **1. Choosing a Server**
	- **Server Type**: For penetration testing, choose the **Cloud Computer** option.
	- **Location**: Select the nearest location to ensure low latency. If testing is on another continent, set up a VPS in that region.
	- **Operating System**: Options include:
	    - ParrotOS (Debian-based).
	    - Ubuntu.
	    - Custom ISO (via public URL).
- #### **2. Performance Level**
	- **Low-cost configurations** (e.g., 1024 MB memory) are suitable for light use.
	- For heavy usage (e.g., hosting multiple services or high network traffic), choose higher memory and CPU configurations.
	- Test load on a local VM before deployment.
- #### **3. Optional Features**
	- **IPv6**: Recommended to bypass IPv4-only firewalls.
	- **Backups**: Enable automatic backups for data safety.
	- **Private Networking & DDoS Protection**: Consider enabling these for additional security.



### **4. Generating SSH Keys**
- SSH keys provide secure, password-free access to the VPS.
- **Command to Generate SSH Keys**:
```bash
ssh-keygen -t rsa -b 4096 -f vps-ssh
```
- `vps-ssh`: Private key (keep secure).
- `vps-ssh.pub`: Public key (add to the VPS).
- **Example Output**:
```bash
-rw------- 1 user user 3434 Mar 30 12:23 vps-ssh
-rw-r--r-- 1 user user  741 Mar 30 12:23 vps-ssh.pub
```
- **Add Public Key to Vultr**:
1. Navigate to the Vultr control panel.
2. Paste the content of `vps-ssh.pub` into the SSH key section.



### **5. VPS Access via SSH**
- **Access Using Password**:
```bash
ssh root@<vps-ip-address>
```
- Replace `<vps-ip-address>` with your VPS’s IP.
- Enter the root password to log in.



### **6. Adding a New User**
- For security, avoid running services as the root user.
- **Create a New User with Sudo Privileges**:
```bash
adduser <username>
usermod -aG sudo <username>
su - <username>
```



### **7. Configuring SSH for New User**
1. **Create `.ssh` Directory**:
    ```bash
    mkdir ~/.ssh
    ```
2. **Add Public Key**:
    ```bash
    echo '<vps-ssh.pub>' > ~/.ssh/authorized_keys
    ```
3. **Set Permissions**:
    ```bash
    chmod 600 ~/.ssh/authorized_keys
    ```
- **Access VPS with New User**:
```bash
ssh <username>@<vps-ip-address> -i vps-ssh
```



### **Key Considerations**
1. **Use SSH Keys for Security**: Avoid using password-based logins for regular access.
2. **Enable IPv6**: Enhances connectivity and bypasses IPv4-only restrictions.
3. **Secure Root Access**: After setup, disable root SSH login to enhance security.
4. **Testing Load**: Use a local VM to simulate workloads and optimize performance.

### **VPS Setup with Vultr**
1. **Choosing a Provider and Server Type**:
    - **Provider**: Vultr
    - **Server Type**: For penetration testing, choose the Cloud Computer server.

1. **Selecting Location**:
    - Choose a location close to you for better connectivity.
    - For tests on other continents, you can use automation scripts to set up a VPS in the desired region.

1. **Selecting the Operating System**:
    - Choose an OS like ParrotOS, which is based on Debian, or Ubuntu.
    - For custom OS, upload an ISO via a public link. Copy the link from the ParrotOS website and paste it into Vultr.

1. **Choosing Performance Level**:
    - Performance options affect cost. Choose based on your needs:
        - For advanced use, more than 1024MB memory might be needed.
    - Test the OS and services locally in a VM to assess requirements.

1. **Optional Features**:
    - **IPv6**: Recommended for added security.
    - **Automatic Backups**, **Private Networking**, **DDOS Protection**: Optional but may incur additional costs.

1. **Generating SSH Keys**:
    - Generate SSH keys on your local machine or VM for secure access.
    - ssh-keygen -t rsa -b 4096 -f vps-ssh
	- **Private Key**: `vps-ssh` (Keep this secure and private).
	- **Public Key**: `vps-ssh.pub` (Upload to Vultr).

- **Setting Up VPS**:
    - Insert the public key into the Vultr control panel.
    - Choose a hostname and label for the VPS.

- **Accessing the VPS**:
    - After installation, access the VPS using SSH.

- **Using Password**:
	- ssh root@"vps-ip-address"
	- Enter the password when prompted.

- **Creating a New User**:
	- To avoid running services as root, create a new user with sudo privileges.
		- adduser cry0l1t3
		- usermod -aG sudo cry0l1t3
		- su - cry0l1t3

- **Adding SSH Key for New User**:
	- Switch to the new user and configure SSH key-based authentication.
		- mkdir ~/.ssh
		- echo '<vps-ssh.pub>' > ~/.ssh/authorized_keys
		- chmod 600 ~/.ssh/authorized_keys

- **Accessing the VPS with SSH Keys**:
	- Use the private key to log in as the new user.
	- ssh cry0l1t3@"vps-ip-address" -i vps-ssh
A Virtual Private Server (VPS) is critical for penetration testing as it allows storing and accessing resources from anywhere with an internet connection. We can use something like Vultr for pen-testing purposes.

#### Why Use a VPS for Pen-Testing:
- **Centralized Resource Access**: A VPS serves as a hub to store resources, accessible from any location.
- **Simulating Different Geographies**: VPS can be set up in different regions for localized penetration testing.
- **Pre-configured Testing Environment**: Saves time by maintaining ready-to-use environments for testing exploits before deploying them on real targets.

#### VPS Setup Steps (Vultr Example):
1. **Choose the Server Type**:
    - Vultr offers various servers, and for pen-testing, the **Cloud Compute server** is typically sufficient.
2. **Location Selection**:
    - Select the server location closest to you for optimal connectivity. You can set up multiple VPSs in different locations for penetration testing across regions.
3. **Choose Operating System**:
    - You can choose pre-configured systems like **ParrotOS** or **Ubuntu**.
    - For more control, upload a custom ISO via a public link (e.g., from ParrotOS mirrors).
4. **Select Performance Level**:
    - For basic pen-testing, a lower-tier VPS (e.g., 1024MB RAM) can be sufficient.
    - For more advanced usage, consider scaling up resources (RAM, CPU) based on service load.
5. **Enable IPv6**:
    - Many firewalls focus on IPv4 protection, so enabling IPv6 can help bypass them during penetration tests.
6. **Additional Options**:
    - **Automatic backups**: Adds redundancy in case of failure.
    - **DDOS protection**: Useful for securing your VPS.

#### Setting Up SSH Access:
1. **Generate SSH Keys**:
    - SSH keys are essential for secure access to your VPS. Here’s how to generate a pair on your local machine:
```
ssh-keygen -t rsa -b 4096 -f vps-ssh
```
- The **private key** (`vps-ssh`) should be kept secure.
- The **public key** (`vps-ssh.pub`) is added to the Vultr control panel.

**Adding SSH Key to VPS**:
- After generating the SSH key, add the public key to the **authorized_keys** file on the VPS:
```
mkdir ~/.ssh
echo '<vps-ssh.pub>' > ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
```

**SSH Access**:
- Use your private key to log into the VPS via SSH:
```
ssh cry0l1t3@<vps-ip-address> -i vps-ssh
```

#### Adding a New Sudo User:
1. **Create New User**:
    - Avoid running services as `root`. Add a new sudo user:
```
adduser cry0l1t3
usermod -aG sudo cry0l1t3
su - cry0l1t3
```
**Add Public SSH Key for the New User**:
- Set up SSH key-based login for the new user by copying the public key to their authorized keys file.
```
mkdir ~/.ssh
echo '<vps-ssh.pub>' > ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
```

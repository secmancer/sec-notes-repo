### Linux for Penetration Testing
- #### **Introduction**
	- Linux is the most widely used Operating System (OS) for penetration testing.
	- Familiarity with Linux is crucial to ensure efficiency during penetration tests, as it saves time that could otherwise be lost in system configuration.
	- It's best to prepare a standardized system setup in advance to maintain consistency in your testing environment.



### Penetration Testing Distributions
- #### **Choosing the Right Distribution**
	- Various Linux distributions can be used for penetration testing, each with its advantages and disadvantages.
	- The choice of distribution depends on individual needs and preferences, as the tools installed on these systems can be transferred to other distributions.
	- Ideal penetration testing distributions have:
	    - Large, active communities
	    - Comprehensive, detailed documentation
	- Popular distributions:
	    - **ParrotOS (Pwnbox)**
	    - **Kali Linux**
	    - **BlackArch**
	    - **BackBox**
- In this guide, we focus on **ParrotOS Security** for penetration testing.



### VM Setup for ParrotOS Installation
- #### **Steps to Set Up a Virtual Machine (VM)**
	1. **VM Software**: Use VMware Workstation (or preferred software).
	2. **ISO Selection**: Choose the ParrotOS ISO file for installation.
	3. **VM Configuration**:
	    - Set the base OS to **Debian-based** (for ParrotOS).
	    - Name your VM and define the storage path.
	    - Set the VM size, ensuring it's **greater than 20 GB** for future tool installations.
	    - Opt to save the VM as a **single file** for easier management.



### Installing ParrotOS
- #### **Installation Steps**
	1. **Boot the VM** and access the GRUB menu to select **ParrotOS** for installation.
	2. **Mouse Control**: To release the mouse from the VM window, press **[CTRL] + [ALT]**.
	3. **Language and Keyboard Settings**: Select your language, location, and keyboard preferences.
	4. **Partitioning**: Choose **Logical Volume Manager (LVM)** for data encryption and partition management. Opt to create a **Swap** partition without Hibernate.
	    - LVM provides an abstraction layer for flexible disk management, supporting RAID-like functionality.
	5. **Set User Info**: Configure the username, hostname, and password.
	6. **Disk Encryption**: For added security, enable **LUKS encryption** with a strong passphrase. Use a password manager to securely store it.
	7. **Final Setup**: Review partition settings and proceed with installation.
-  #### **Post-Installation**
	- After installation, the system will prompt for the encryption passphrase. If entered correctly, the system will boot and you can log in with your created credentials.



### System Updates & Package Management
- #### **Updating the System**
- Use **APT** (Advanced Packaging Tool) to update and manage packages.
    - **Update Command**:
        ```
        sudo apt update -y && sudo apt full-upgrade -y && sudo apt autoremove -y && sudo apt autoclean -y
        ```    
    - This will ensure your system is up to date and free from unnecessary packages.
- #### **APT Sources List**
	- The **ParrotOS sources list** (`/etc/apt/sources.list.d/parrot.list`) includes repositories for ParrotOS packages.



### Installing Tools
- #### **Available Tools List**
	- ParrotOS comes with a variety of pre-installed tools:
	    - **Networking**: netcat, ncat, nmap, wireshark
	    - **Hacking**: hashcat, hydra, metasploit-framework
	    - **Reconnaissance**: sqlmap, gobuster, theharvester
	    - **Remote Access**: remmina, xfreerdp, crackmapexec
	    - **Miscellaneous**: exiftool, curl, vim, tmux
- #### **Installing Tools Manually**
	- To install specific tools, run:
    ```
    sudo apt install netcat ncat nmap wireshark tcpdump git vim tmux -y
    ```
- #### **Installing from a List**
	- If you have a list of tools to install, you can use:
    ```
    sudo apt install $(cat tools.list | tr "\n" " ") -y
    ```
    


### Using GitHub for Tools Not in Repositories
- #### **Cloning Repositories**
	- If tools aren't available in repositories, you can clone them from GitHub. For example, to download the **Privilege Escalation Awesome Scripts Suite**:
    ```
    git clone https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite.git
    ```
- #### **Listing Cloned Files**
	- After cloning, list the repository contents to ensure successful download:
    ```
    ls -l privilege-escalation-awesome-scripts-suite/
    ```
    


### Snapshotting Your VM
- #### **Why Take Snapshots?**
	- Snapshots allow you to save the current state of the VM, making it easier to revert to a stable configuration if things go wrong during testing or configuration changes.
- #### **Creating Snapshots**
	- After completing major configuration stages, **shut down** the OS to take a snapshot efficiently.
	- Name the snapshot "Initial Setup" to mark the stable state.
	- Periodically take snapshots during penetration tests for quick recovery.



### **Conclusion**
- Preparing a standardized and secure system environment like ParrotOS for penetration testing is crucial for efficiency.
- Take the time to configure your VM, install necessary tools, and manage your packages properly.
- Always back up your setup with snapshots to avoid loss of progress during the penetration testing process.
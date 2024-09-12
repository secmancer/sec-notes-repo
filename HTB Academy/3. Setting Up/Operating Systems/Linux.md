Linux is the most widely used OS for penetration testing.
- Familiarity with Linux is crucial to avoid wasting time during an actual penetration test.

**Preparing a Standard OS Setup:**
- Developing a consistent setup ensures efficiency and saves time.
- Pre-configure a system before a penetration test to avoid delays in tool installation during the testing phase.

**Penetration Testing Distributions:**
- Different distributions offer unique features, but the choice depends on personal preference.
- Most popular distributions for penetration testing:
    - ParrotOS (Pwnbox)
    - Kali Linux
    - BlackArch
    - BackBox

**ParrotOS Security** is used as the example distribution in this guide.

**Setting up the Virtual Machine (VM):**
- Use VMware Workstation and specify the ParrotOS ISO file.
- Since VMware might not recognize the OS, manually select "Debian-based" during installation.

**VM Configuration:**
- Assign a name and storage location for the VM.
- Recommended disk size: more than 20 GB to accommodate growing packages and applications.
- Save the VM as a single file for easier future migration.

**ParrotOS Installation:**
- In the GRUB menu, select the installation option.
- If VMware captures the mouse in the window, release it with `[CTRL] + [ALT]`.
- During installation, configure the language, location, keyboard, and partition settings.
- Encrypt the system with **LVM (Logical Volume Manager)** for better security.
- Use a strong passphrase for encryption and store it securely in a password manager.

**Logical Volume Manager (LVM):**
- Provides dynamic partitions and can span across multiple disks.
- Ensure encryption is set up during partitioning and verify the passphrase.

**Finishing the Installation:**
- Complete the partition setup and proceed with the installation.
- Restart the VM and input the passphrase to unlock the system.
- Log in with the username and password created during setup.

**Updating the System with APT Package Manager:**
- Use APT to manage package installations and updates.
- APT retrieves packages from sources listed in `/etc/apt/sources.list.d/parrot.list`.
```
sudo apt update -y && sudo apt full-upgrade -y && sudo apt autoremove -y && sudo apt autoclean -y
```

**Installing Penetration Testing Tools:**
- Key tools to install: `netcat`, `nmap`, `wireshark`, `tcpdump`, `hashcat`, `hydra`, etc.
- For a small list, manually input tools into the install command:
```
sudo apt install netcat nmap wireshark tcpdump git vim tmux -y
```
- For larger toolsets, create a list and use it for batch installation:
```
sudo apt install $(cat tools.list | tr "\n" " ") -y
```


**Installing Tools from GitHub:**
- For tools not available in repositories, clone them from GitHub.
- Example: Cloning **Privilege-Escalation-Awesome-Scripts-Suite**:
```
git clone https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite.git
```

**Taking a VM Snapshot:**
- After installing tools and configurations, take a snapshot for easy rollback in case of errors.
- Shut down the VM before creating a snapshot to reduce time.
- Name the snapshot "Initial Setup" for easy identification.
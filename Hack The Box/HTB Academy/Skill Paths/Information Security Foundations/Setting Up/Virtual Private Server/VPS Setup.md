### Introduction
- A VPS is crucial for internal and external penetration tests, storing resources and providing remote access from almost anywhere with internet access.
- Setting up the VPS involves configuring the folder structure and services, with Vultr as an example provider offering nearly identical configurations to others.
- In Vultr, we select a `Cloud Compute` server, ensuring optimal connection by choosing the closest server location.
- For the operating system, we can choose ParrotOS (based on Debian) or upload our own ISO via a public link from sites like the [ParrotOS website](https://www.parrotsec.org/security-edition/).
- Select the performance level based on the VPS’s intended use, balancing cost and resource needs. Use a local VM to test OS loads before final configuration.
- Consider using IPv6, as many firewalls still focus on IPv4, enhancing security. Options like automatic backups, private networking, and DDOS protection are available at additional costs.
- Generate SSH keys during setup for secure remote access, which can also be generated later on the VPS, VM, or host system.


### Generate SSH Keys
```shell-session
┌─[cry0l1t3@parrot]─[~]
└──╼ $ ssh-keygen -t rsa -b 4096 -f vps-ssh

Generating public/private rsa key pair.
Enter passphrase (empty for no passphrase): ******************
Enter same passphrase again: ******************
Your identification has been saved in vps-ssh
Your public key has been saved in vps-ssh.pub
The key fingerprint is:
SHA256:zXyVAWK00000000000000000000VS4a/f0000+ag cry0l1t3@parrot
The key's randomart image is:
...SNIP...
```
- With the command shown above, we generate two different keys. 
- The `vps-ssh` is the `private key` and must not be shared anywhere or with anyone. 
- The second `vps-ssh.pub` is the `public key` which we can now insert in the Vultr control panel.


### SSH Keys
```shell-session
┌─[cry0l1t3@parrot]─[~]
└──╼ $ ls -l vps*

-rw------- 1 cry0l1t3 cry0l1t3 3434 Mar 30 12:23 vps-ssh
-rw-r--r-- 1 cry0l1t3 cry0l1t3  741 Mar 30 12:23 vps-ssh.pub
```
- Finally, we choose a hostname and the server label with which we want to name our VPS.
- Once the VPS is installed, we can access it via SSH.


### SSH Using Password
```shell-session
secmancer@htb[/htb]$ ssh root@<vps-ip-address>

root@<vps-ip-address>'s password: 

[root@VPS ~]# 
```
- After that, we should add a new user for the VPS to not run our services with root or administrator privileges. 
- For this, we can then generate another SSH key and insert it for this user.


### Adding a New Sudo User
```shell-session
[root@VPS ~]# adduser cry0l1t3
[root@VPS ~]# usermod -aG sudo cry0l1t3
[root@VPS ~]# su - cry0l1t3
Password: 

[cry0l1t3@VPS ~]$
```


### Adding Public SSH Key to VPS
```shell-session
[cry0l1t3@VPS ~]$ mkdir ~/.ssh
[cry0l1t3@VPS ~]$ echo '<vps-ssh.pub>' > ~/.ssh/authorized_keys
[cry0l1t3@VPS ~]$ chmod 600 ~/.ssh/authorized_keys
```
- Once we have added this to the `authorized_keys` file, we can use the `private key` to log in to the system via SSH.


### Using SSH Keys
```shell-session
secmancer@htb[/htb]$ ssh cry0l1t3@<vps-ip-address> -i vps-ssh

[cry0l1t3@VPS ~]$ 
```
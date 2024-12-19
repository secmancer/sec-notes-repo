### Introduction
- **Remote Desktop Protocols**: These protocols allow graphical remote access to systems, commonly used for troubleshooting, software/system upgrades, and remote administration.
- **Common Protocols**:
    - **RDP (Remote Desktop Protocol)**: Primarily used for remote access to Windows systems.
    - **VNC (Virtual Network Computing)**: Often used for remote access to Linux systems.
- **Administrator Usage**: Administrators connect to remote systems using the appropriate protocol for tasks like installing applications or performing system maintenance.



### XServer
- **XServer & X11 Protocol**: The XServer is the user-side part of the X Window System (X11), a protocol that enables graphical user interfaces (GUIs) on Unix-based systems and other OSes. It facilitates communication between the desktop environment and the operating system.
- **Network Transparency**: X11 supports network transparency, allowing the XServer to run on one machine while the graphical user interface can be displayed on another, even over a network.
- **Ports & Communication**: XServer uses ports in the `TCP/6000-6009` range for communication. Port 6000 is used for the first X display (`:0`), enabling client-server interaction for applications.
- **Remote Access**: X11 allows remote access to applications, enabling users to access graphical interfaces across systems without needing additional protocols like VNC or RDP, which handle graphical output over the network.
- **Tunneling for Security**: X11 communication is unencrypted by default but can be secured using SSH tunneling. Enabling X11 forwarding in SSH (`/etc/ssh/sshd_config`) ensures secure data transmission between client and server.



### X-11 Forwarding
```shell-session
secmancer@htb[/htb]$ cat /etc/ssh/sshd_config | grep X11Forwarding

X11Forwarding yes
```
- With this we can start the application from our client with the following command.
```shell-session
secmancer@htb[/htb]$ ssh -X htb-student@10.129.23.11 /usr/bin/firefox

htb-student@10.129.14.130's password: ********
<SKIP>
```



### X11 Security
- **X11 Security Risks**: X11 is an insecure protocol by default because it transmits data unencrypted. This allows anyone on the network to potentially access sensitive information, such as reading window contents, capturing keystrokes, taking screenshots, or controlling the mouse cursor without the user's awareness.
- **Exploitation by Penetration Testers**: With tools like `xwd` and `xgrabsc`, penetration testers could potentially read users' keystrokes, capture screenshots, or inject keystrokes over the network.
- **Vulnerabilities in XServer**: Security flaws in XServer have allowed local attackers to exploit vulnerabilities (e.g., CVE-2017-2624, CVE-2017-2625, CVE-2017-2626) to execute arbitrary code and gain user privileges. These vulnerabilities affected UNIX and Linux distributions such as Red Hat Enterprise Linux, Ubuntu, and SUSE Linux.



### XDMCP
- **XDMCP Protocol**: The `X Display Manager Control Protocol` (XDMCP) is used by the X Display Manager to manage remote X Window sessions via UDP port 177. It allows system administrators to provide remote desktop access to X terminals in Unix/Linux environments.
- **Insecurity of XDMCP**: XDMCP is an insecure protocol and should not be used in high-security environments. It can be exploited in various ways, including through man-in-the-middle attacks, where an attacker intercepts and impersonates parties involved in the communication.
- **Potential Exploitation**: In a man-in-the-middle attack, the attacker could gain unauthorized access to the server, run arbitrary commands, and access sensitive data, potentially compromising system security.
- **XDMCP Server Setup**: For a Linux system to act as an XDMCP server, it must have a graphical user interface (GUI) like KDE or GNOME installed and configured. This setup allows remote clients to access the GUI.



### VNC
- **VNC Overview**: `Virtual Network Computing` (VNC) is a remote desktop sharing system based on the RFB protocol, allowing users to control a computer remotely and interact with its desktop environment as if physically present. It's a common protocol for remote graphical connections on Linux hosts.
- **Security**: VNC is generally secure, using encryption to protect data in transit and requiring authentication before access. It's commonly used for troubleshooting, server maintenance, remote application access, and collaborative screen sharing.
- **VNC Server Types**: There are two main types of VNC servers:
    - One displays the host computer's screen for remote support.
    - The other allows users to log into virtual sessions, similar to terminal servers.
- **Availability**: VNC server and viewer programs are available for all major operating systems, making it widely used in IT services. Similar tools include proprietary TeamViewer and RDP.
- **Default Ports**: The VNC server typically listens on TCP port 5900 for `display 0`, with additional displays accessible through ports 5901, 5902, etc.
- **Popular VNC Tools**:
    - [TigerVNC](https://tigervnc.org/)
    - [TightVNC](https://www.tightvnc.com/)
    - [RealVNC](https://www.realvnc.com/en/)
    - [UltraVNC](https://uvnc.com/)
- UltraVNC and RealVNC are often preferred for their encryption and security features.
- **Example Setup**: For a TigerVNC server setup, installing `XFCE4` as the desktop manager is recommended for stability, as GNOME can be unstable with VNC. Necessary packages should be installed, and a password must be created for the VNC connection.



### TigerVNC Installation
```shell-session
htb-student@ubuntu:~$ sudo apt install xfce4 xfce4-goodies tigervnc-standalone-server -y
htb-student@ubuntu:~$ vncpasswd 

Password: ******
Verify: ******
Would you like to enter a view-only password (y/n)? n
```
- During installation, a hidden folder is created in the home directory called `.vnc`. 
- Then, we have to create two additional files, `xstartup` and `config`. 
- The `xstartup` determines how the VNC session is created in connection with the display manager, and the `config` determines its settings.
- #### Configuration
```shell-session
htb-student@ubuntu:~$ touch ~/.vnc/xstartup ~/.vnc/config
htb-student@ubuntu:~$ cat <<EOT >> ~/.vnc/xstartup

#!/bin/bash
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
/usr/bin/startxfce4
[ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup
[ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
x-window-manager &
EOT
```
```shell-session
htb-student@ubuntu:~$ cat <<EOT >> ~/.vnc/config

geometry=1920x1080
dpi=96
EOT
```
- Additionally, the `xstartup` executable needs rights to be started by the service.
```shell-session
htb-student@ubuntu:~$ chmod +x ~/.vnc/xstartup
```
- Now we can start the VNC server.
- #### Start the VNC server
```shell-session
htb-student@ubuntu:~$ vncserver

New 'linux:1 (htb-student)' desktop at :1 on machine linux

Starting applications specified in /home/htb-student/.vnc/xstartup
Log file is /home/htb-student/.vnc/linux:1.log

Use xtigervncviewer -SecurityTypes VncAuth -passwd /home/htb-student/.vnc/passwd :1 to connect to the VNC server.
```
- In addition, we can also display the entire sessions with the associated ports and the process ID.
- #### List Sessions
```shell-session
htb-student@ubuntu:~$ vncserver -list

TigerVNC server sessions:

X DISPLAY #     RFB PORT #      PROCESS ID
:1              5901            79746
```
- To encrypt the connection and make it more secure, we can create an SSH tunnel over which the whole connection is tunneled. 
- How tunneling works in detail we will learn in the [Pivoting, Tunneling, and Port Forwarding](https://academy.hackthebox.com/module/details/158) module.
- #### Setting Up an SSH Tunnel
```shell-session
secmancer@htb[/htb]$ ssh -L 5901:127.0.0.1:5901 -N -f -l htb-student 10.129.14.130

htb-student@10.129.14.130's password: *******
```
- Finally, we can connect to the server through the SSH tunnel using the `xtightvncviewer`.



### Connecting to the VNC Server
```shell-session
secmancer@htb[/htb]$ xtightvncviewer localhost:5901

Connected to RFB server, using protocol version 3.8
Performing standard VNC authentication

Password: ******

Authentication successful
Desktop name "linux:1 (htb-student)"
VNC server default format:
  32 bits per pixel.
  Least significant byte first in each pixel.
  True colour: max red 255 green 255 blue 255, shift red 16 green 8 blue 0
Using default colormap which is TrueColor.  Pixel format:
  32 bits per pixel.
  Least significant byte first in each pixel.
  True colour: max red 255 green 255 blue 255, shift red 16 green 8 blue 0
Same machine: preferring raw encoding
```
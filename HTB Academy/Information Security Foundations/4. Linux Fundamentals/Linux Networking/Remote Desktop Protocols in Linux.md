### Remote Desktop Protocols Overview
- **Purpose**: Remote desktop protocols provide graphical remote access to a system for tasks like troubleshooting, software/system upgrades, and remote administration.
- **Usage**: Administrators use protocols like RDP (Windows) and VNC (Linux) to connect and administer systems remotely, install applications, or manage systems.


### XServer (X Window System)
- **Function**: XServer is part of the X Window System (X11), enabling graphical user interfaces on Unix/Linux systems, and allows for remote graphical access via TCP/IP or Unix sockets.
- **Network Transparency**: X11 allows rendering on the local computer, reducing traffic and load on remote systems compared to protocols like VNC and RDP, which render output on the remote computer.
- **Ports**: XServer typically uses TCP ports 6001–6009 for communication between the client and server, with port 6000 for the first X display (:0).
- **Security Concern**: X11 transmits data unencrypted, but this can be mitigated by tunneling through SSH (`X11Forwarding yes` in `/etc/ssh/sshd_config`).

### X11 Security
- **Vulnerabilities**: X11 has inherent security risks due to unencrypted communication, which can be exploited to read user data or perform actions unnoticed. Vulnerabilities such as CVE-2017-2624, CVE-2017-2625, and CVE-2017-2626 have affected XServer.
- **Mitigation**: Tunneling X11 through SSH provides encryption and protects against these vulnerabilities.


### XDMCP (X Display Manager Control Protocol)
- **Purpose**: XDMCP manages remote X Window sessions over UDP port 177, allowing full GUI redirection from the server to the client.
- **Security Issue**: XDMCP is insecure and vulnerable to man-in-the-middle attacks. It should be avoided in environments requiring high security.


### VNC (Virtual Network Computing)
- **Function**: VNC allows users to control remote systems graphically via the RFB protocol. It supports collaboration, remote access, troubleshooting, and administration.
- **Security**: VNC supports encryption and authentication for secure connections.
- **Ports**: VNC servers typically use port 5900 for the first display, with subsequent displays using higher ports (e.g., 5901, 5902).
- **Tools**: Common VNC tools include TigerVNC, TightVNC, RealVNC, and UltraVNC, with RealVNC and UltraVNC being favored for their enhanced security.

### VNC Server Setup Example (TigerVNC)
1. **Install Dependencies**:
```
sudo apt install xfce4 xfce4-goodies tigervnc-standalone-server -y
vncpasswd
```
2. **Configure Startup and Settings:**
```
touch ~/.vnc/xstartup ~/.vnc/config
chmod +x ~/.vnc/xstartup
```
	- Add to `~/.vnc/xstartup`:
```
#!/bin/bash
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
/usr/bin/startxfce4
```
	- Add to `~/.vnc/config`:
```
geometry=1920x1080
dpi=96
```
3. **Start VNC Server**:
```
vncserver
vncserver -list
```
4. **Create SSH Tunnel**:
```
ssh -L 5901:127.0.0.1:5901 -N -f -l htb-student 10.129.14.130
```
5. **Connect to VNC**:
```
xtightvncviewer localhost:5901
```
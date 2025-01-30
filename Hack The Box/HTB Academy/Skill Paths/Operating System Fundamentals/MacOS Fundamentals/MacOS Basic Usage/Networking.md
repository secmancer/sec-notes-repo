### Introduction
- **Networking** is crucial for any operating system, including macOS.
- **Three main ways** to manage networking on macOS:
  1. **Terminal (CLI)**
  2. **System Settings** (formerly System Preferences)
  3. **Control Center**



### Basics
- **Administrative privileges** may be required to manage networking settings.
- **Validate Networking Hardware**:
  - Check active network interfaces using the **System Information** application.
    - Access via **Spotlight** or **Launchpad**.
    - Navigate to the **Networking tab** to view active interfaces and details.



### System Settings
- **System Preferences** renamed to **System Settings** in macOS 13 (Ventura).
  - Redesigned to resemble iOS/iPadOS.
  - Use the **search function** to locate settings.
- **Network Tab**:
  - View and manage network devices.
  - **Advanced** button provides detailed interface configuration.
    - Modify settings like **IP address** (e.g., switch from DHCP to manual).
    - **Apply** changes to persist.



### Control Center
- Quick access to networking settings.
- Toggle interfaces on/off or customize settings via **System Settings**.



### Managing Networking via CLI
- #### 1. **ifconfig**
	- **Command**: `ifconfig`
	  - Displays all network interfaces and their configurations.
	  - Example:
    ```bash
    lo0: flags=8049<UP,LOOPBACK,RUNNING,MULTICAST> mtu 16384
    en0: flags=8863<UP,BROADCAST,SMART,RUNNING,SIMPLEX,MULTICAST> mtu 1500
    ```
  - Filter output by specifying an interface: `ifconfig en0`.
- **Set Manual IP**:
  ```bash
  ifconfig en0 inet 192.168.1.1 netmask 255.255.255.0
  ```
  - **Note**: Changes are temporary and will not persist after reboot.
- #### 2. **lsof**
	- **Command**: `lsof -n -i4TCP -P`
	  - Lists applications bound to TCP ports (IPv4).
	  - Example:
    ```bash
    COMMAND    PID USER   FD   TYPE  DEVICE SIZE/OFF NODE NAME
    launchd      1 root    9u  IPv4  0xdc22 0t0      TCP 127.0.0.1:22 (LISTEN)
    ```
  - Useful for diagnosing network issues.
- #### 3. **networksetup**
	- **Commands**:
	  - List all network services: `networksetup -listallnetworkservices`.
	  - List network service order: `networksetup -listnetworkserviceorder`.
	  - Get info about a service: `networksetup -getinfo Wi-Fi`.
	  - Set manual IP: `networksetup -setmanual <networkservice> <ip> <netmask> <gateway>`.
	- **Example**:
  ```bash
  networksetup -getinfo Wi-Fi
  ```



### Tips & Tricks
- #### 1. **Network Quality**
	- **Command**: `networkQuality -I <interface>`
	  - Provides live feedback on network performance.
	  - Example:
    ```bash
    Downlink: capacity 104.874 Mbps, responsiveness 66 RPM
    ```
- #### 2. **Find Wi-Fi Password**
	- **Command**: `security find-generic-password -wa <SSID>`
	  - Retrieves the password for a previously connected Wi-Fi network.
	  - Example:
    ```bash
    security find-generic-password -wa Office-2.4G
    Sup3r$ecure
    ```



### VPNs on macOS
- #### 1. **Tunnelblick**
	- **Free and open-source** VPN client.
	- Works with **OpenVPN** config files.
	- Supports persistent connections and advanced configurations.
- #### 2. **Viscosity**
	- **Paid option** ($14 one-time purchase).
	- Intuitive interface with live network statistics.
- #### 3. **Other Options**
	- **OpenVPN**: Official macOS client.
	- **VPN Providers**: Many offer macOS-compatible software.



### Bonjour
- **Apple's zero-configuration networking** protocol.
- Automatically discovers devices and services on a network.
- **Security Considerations**:
  - Devices using Bonjour can be accessed by others on the same network.
  - Use **network segmentation** and **authentication** to mitigate risks.



### Summary
- **System Settings** is the recommended method for managing networking on macOS.
- **CLI tools** like `ifconfig`, `lsof`, and `networksetup` provide advanced control.
- **Tips** like `networkQuality` and `security` commands simplify common tasks.
- **VPNs** like Tunnelblick and Viscosity are essential for secure remote connections.
- **Bonjour** simplifies device discovery but requires proper security measures.
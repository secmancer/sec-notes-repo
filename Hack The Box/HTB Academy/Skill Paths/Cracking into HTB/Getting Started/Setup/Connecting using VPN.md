### What is a VPN?
- **Definition**: A secured communication channel over public networks allowing access to private networks.
- **Purpose**: Encrypts communication to prevent eavesdropping and appears to originate from the VPN server's IP address.



### Types of Remote Access VPNs:
1. **SSL VPN**:
    - Uses a web browser as the client.
    - Grants access to web-based apps or internal networks without specialized software.
2. **Client-Based VPN**:
    - Requires installation of VPN client software.
    - Simulates direct connection to the private network with access determined by server configuration.



### Use Cases for VPN:
- **Privacy & Security**:
    - Obscure browsing traffic and disguise IP addresses.
    - Protect against hostile networks (e.g., public Wi-Fi).
- **Risks**:
    - VPN providers may log data or not follow security best practices.
    - Does not guarantee anonymity or protection against consequences of illegal activities.



### HTB VPN Connection Guidelines:
- **Considerations**:
    - Treat the network as hostile.
    - Use a virtual machine and enhance security (e.g., disable SSH password authentication).
    - Avoid leaving sensitive information on attack VMs.



### Commands for Connecting to HTB VPN:
1. **Connect using OpenVPN**:    
    ```bash
    sudo openvpn user.ovpn
    ```
    - Confirms successful connection with the message: `Initialization Sequence Completed`.
2. **Verify VPN Connection**:
    - Check for `tun0` adapter:
        ```bash
        ifconfig
        ```
    - Inspect routing table:
        ```bash
        netstat -rn
        ```



### Example Output for Verification:
1. **`ifconfig` Output**:
    ```
    tun0: flags=4305<UP,POINTOPOINT,RUNNING,NOARP,MULTICAST> mtu 1500
    inet 10.10.x.2 netmask 255.255.254.0 destination 10.10.x.2
    ```
2. **`netstat -rn` Output**:
    ```
    Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
    10.10.14.0      0.0.0.0         255.255.254.0   U         0 0          0 tun0
    ```



### Additional Resources:
- Hack The Box support portal articles:
    - **Introduction to Lab Access**
    - **Connection Troubleshooting**

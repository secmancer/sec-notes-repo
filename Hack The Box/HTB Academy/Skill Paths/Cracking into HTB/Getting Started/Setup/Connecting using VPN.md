- [Virtual private network (VPN)](https://en.wikipedia.org/wiki/Virtual_private_network) allows for connections to a private (internal) network to access hosts and resources as like we are connected on the same network.
	- For example, an employee remotely connecting to their company's corporate network from their home allows that employee to get work done like they are on the corporate network in a secure fashion.
- Additionally provides a degree of privacy and security through encrypting communications over the channel to prevent eavesdropping on data traversing through it.
![[GettingStarted.png]]
- VPNs, at a high level, route our device's connection through the target VPN's private server, rather than our internet service provider (ISP). 
- When connected, data comes from the VPN server instead of our computer, so we will have a different public IP address assigned to us.
- There are two main types of remote access VPNs: client-based VPN and SSL VPN. SSL VPN uses the web browser as the VPN client. 
- Control on aspects like access to web-based applications like email/intranet sites are able to be done easily with a VPN without anything else additional.
- Clients download software to establish this connection for it to function.
- Some corporate VPNs provides employees with full access, while others may assigns users to a specific segment reserved for remote workers.


### Why Use VPNs?
- `NordVPN` or `Private Internet Access` are VPN services we can subscribe to. These allow us to connect to various VPN servers in other parts of the world.
	- While this might provide some security/privacy benefit to us, there is always the great chance that your data is being logged, or even that you are trusting that the service uses the best security practices possible, which isn't always easy to tell from our end.
	- Therefore, there is always some level of risk when doing this avenue.
- Usage of these VPN service are more useful for bypassing certain network/firewall restrictions or when connected to a possible hostile network, like public Wi-Fi. 
- Therefore, don't use these services for anything illegal. By law, they are required to work with law enforcement agencies on this kind of thing.

### Connecting to the HTB VPN
- To access HTB, a VPN connection is available to us. Note that this is intended only for VMs/targets that are in the scope of learning. Basically, no funny business while connected.
- if using the AttackBox, we don't have to worry. This is automatically handled for us.
- However, we want to use our own toolset/VM, then additional setup is required.
- Downloading our VPN configuration file, we can connect using OpenVPN, one of many different VPN tools, by running the following command:
```
secmancer@htb[/htb]$ sudo openvpn user.ovpn

Thu Dec 10 18:42:41 2020 OpenVPN 2.4.9 x86_64-pc-linux-gnu [SSL (OpenSSL)] [LZO] [LZ4] [EPOLL] [PKCS11] [MH/PKTINFO] [AEAD] built on Apr 21 2020
Thu Dec 10 18:42:41 2020 library versions: OpenSSL 1.1.1g  21 Apr 2020, LZO 2.10
Thu Dec 10 18:42:41 2020 Outgoing Control Channel Authentication: Using 256 bit message hash 'SHA256' for HMAC authentication
Thu Dec 10 18:42:41 2020 Incoming Control Channel Authentication: Using 256 bit message hash 'SHA256' for HMAC authentication
Thu Dec 10 18:42:41 2020 TCP/UDP: Preserving recently used remote address: [AF_INET]
Thu Dec 10 18:42:41 2020 Socket Buffers: R=[212992->212992] S=[212992->212992]
Thu Dec 10 18:42:41 2020 UDP link local: (not bound)
<SNIP>
Thu Dec 10 18:42:41 2020 Initialization Sequence Completed
```
- `Initialization Sequence Completed` lets us know we successfully connected to it.
- Therefore, typing `ifconfig`, we are given `tun` adapter to demonstrate our connection.
```
secmancer@htb[/htb]$ ifconfig

<SNIP>

tun0: flags=4305<UP,POINTOPOINT,RUNNING,NOARP,MULTICAST>  mtu 1500
        inet 10.10.x.2  netmask 255.255.254.0  destination 10.10.x.2
        inet6 dead:beef:1::2000  prefixlen 64  scopeid 0x0<global>
        inet6 fe80::d82f:301a:a94a:8723  prefixlen 64  scopeid 0x20<link>
        unspec 00-00-00-00-00-00-00-00-00-00-00-00-00-00-00-00  txqueuelen
```
- We can show ourselves networks accessible within the VPN by running `netstat -rn`.
```
secmancer@htb[/htb]$ netstat -rn

Kernel IP routing table
Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
0.0.0.0         192.168.1.2     0.0.0.0         UG        0 0          0 eth0
10.10.14.0      0.0.0.0         255.255.254.0   U         0 0          0 tun0
10.129.0.0      10.10.14.1      255.255.0.0     UG        0 0          0 tun0
192.168.1.0     0.0.0.0         255.255.255.0   U         0 0          0 eth0
```
- Here, the 10.129.0.0/16 network, intended for HTB Academy machines, can be accessed by the `tun0` adapter via the 10.10.14.0/23 network.
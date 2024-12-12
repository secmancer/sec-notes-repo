### VPN Issues
- First, we should check if we have a connection to the HTB network.
- #### Still Connected to VPN
	- Easiest way is seeing if we have a `Initialization Sequence Completed`message:
```shell-session
secmancer@htb[/htb]$ sudo openvpn ./htb.ovpn

...SNIP...

Initialization Sequence Completed
```
- #### Getting VPN Address
	- We can also check by attempting to get our `tun0` address:
```shell-session
secmancer@htb[/htb]$ ip -4 a show tun0

6: tun0: <POINTOPOINT,MULTICAST,NOARP,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UNKNOWN group default qlen 500
    inet 10.10.10.1/23 scope global tun0
       valid_lft forever preferred_lft forever
```

- If we get our IP back, then we should be connected.
- #### Checking Routing Table
	- We can use the command `sudo netstat -rn` to view our routing table:
```shell-session
secmancer@htb[/htb]$ sudo netstat -rn

[sudo] password for user: 

Kernel IP routing table
Destination     Gateway         Genmask         Flags   MSS Window  irtt Iface
0.0.0.0         192.168.195.2   0.0.0.0         UG        0 0          0 eth0
10.10.14.0      0.0.0.0         255.255.254.0   U         0 0          0 tun0
10.129.0.0      10.10.14.1      255.255.0.0     UG        0 0          0 tun0
192.168.1.0   0.0.0.0         255.255.255.0   U         0 0          0 eth0
```
- #### Pinging Gateway
	- Here, we can check if we have a connection to the `10.10.14.0/23` network on the `tun0` adapter and confirm we have access to the `10.129.0.0/16` network.
	- From there, we can ping the gateway `10.10.14.1` to confirm access.
```shell-session
secmancer@htb[/htb]$ ping -c 4 10.10.14.1
PING 10.10.14.1 (10.10.14.1) 56(84) bytes of data.
64 bytes from 10.10.14.1: icmp_seq=1 ttl=64 time=111 ms
64 bytes from 10.10.14.1: icmp_seq=2 ttl=64 time=111 ms
64 bytes from 10.10.14.1: icmp_seq=3 ttl=64 time=111 ms
64 bytes from 10.10.14.1: icmp_seq=4 ttl=64 time=111 ms

--- 10.10.14.1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3012ms
rtt min/avg/max/mdev = 110.574/110.793/111.056/0.174 ms
```
- After all of that is situated, then we should be ready to go!


### Attempting to Working on Two Devices
- HTB VPN only provides connection to one device only.

### Checking VPN Region
- Picking a different region or one closer to you may also relieve issues as well.
- This can be changed by going to [HackTheBox](https://app.hackthebox.eu/home) and changing our VPN server location.

> Note: Users with a free subscription only can connect to 1-3 free servers in each region. Users with a VPN subscription can connect to VIP servers, which provide a faster connection with less traffic.

### Additional VPN Troubleshooting
- Detailed guidance on troubleshooting VPN connections are available on this [HackTheBox Help page](https://help.hackthebox.eu/troubleshooting/v2-vpn-connection-troubleshooting).

### Burp Suite Proxy Issue
- [Burp Suite](https://portswigger.net/burp/communitydownload) may cause some issues due to its web application proxy feature.
- #### Not Disabling Proxy
	- Turning the Burp proxy on, it will start to capture our traffic and intercept our requests. 
	- This stops any requests we make in the browser like visiting a webpage from happening, as it's intended for us to scourge through them.
	- Make sure this is turned off if you don't plan on using it.
	- After doing this, we should be able to continue browsing without any issues.

### Changing SSH Key and Password
- If we have issues connecting to SSH servers or to our machine from a remote server, we are able to renew or change our SSH key and password.
- We can do this with the `ssh-keygen` command:
```shell-session
secmancer@htb[/htb]$ ssh-keygen

Generating public/private rsa key pair.
Enter file in which to save the key (/home/parrot/.ssh/id_rsa): 
Enter passphrase (empty for no passphrase):
Enter same passphrase again:

Your identification has been saved in /home/parrot/.ssh/id_rsa
Our public key has been saved in /home/parrot/.ssh/id_rsa.pub
The key fingerprint is:
SHA256:...SNIP... parrot@parrot
The key's randomart image is:
+---[RSA 3072]----+
|            o..  |
|     ...SNIP     |
|     ...SNIP     |
|     ...SNIP     |
|     ...SNIP     |
|     ...SNIP     |
|     ...SNIP     |
|       + +oo+o   |
+----[SHA256]-----+
```

- By default, SSH keys are stored in the `.ssh` folder within our home folder (for example, `/home/htb-student/.ssh`). 
- If we wanted to create an ssh key in a different directory, we could can specify a path when prompted. 
- Encrypting our SSH key with a password is also an option, but we are also able to not set one as well.
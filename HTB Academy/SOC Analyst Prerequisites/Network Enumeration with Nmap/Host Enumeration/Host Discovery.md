## Internal Penetration Testing: Host Discovery with Nmap
### Overview
- When conducting an internal penetration test, the first step is to identify which systems are online within the company's network.
- Various Nmap host discovery options can be used to discover active systems.
- ICMP echo requests are the most effective method for determining if a target is alive.


### Importance of Documentation
- **Store Every Scan**:
    - Documenting each scan is crucial for comparison, documentation, and reporting purposes.
    - Different tools can yield different results, so it's important to track which tool produces which results.

### Nmap Scanning Methods
#### Scan Network Range
- **Command**:
```
secmancer@htb[/htb]$ sudo nmap 10.129.2.0/24 -sn -oA tnet | grep for | cut -d" " -f5
```
- **Results**:
	- Active hosts:
	    - 10.129.2.4
	    - 10.129.2.10
	    - 10.129.2.11
	    - 10.129.2.18
	    - 10.129.2.19
	    - 10.129.2.20
	    - 10.129.2.28
- **Scanning Options**:
    - `10.129.2.0/24`: Target network range.
    - `-sn`: Disables port scanning.
    - `-oA tnet`: Stores results in all formats starting with the name 'tnet'.
- **Note**: This method only works if host firewalls allow ICMP requests. Alternative scanning techniques may be required if ICMP is blocked.


#### Scan IP List
- If provided with an IP list for testing, Nmap can read hosts from a file.
- **IP List Example** (`hosts.lst`):
```
10.129.2.4
10.129.2.10
10.129.2.11
10.129.2.18
10.129.2.19
10.129.2.20
10.129.2.28
```
- **Command**:
```
secmancer@htb[/htb]$ sudo nmap -sn -oA tnet -iL hosts.lst | grep for | cut -d" " -f5
```
- **Results**:
    - Active hosts:
        - 10.129.2.18
        - 10.129.2.19
        - 10.129.2.20
- **Scanning Options**:
    - `-iL`: Reads targets from the provided 'hosts.lst' list.


#### Scan Multiple IPs
- To scan specific multiple IPs:
- **Command**:
```
secmancer@htb[/htb]$ sudo nmap -sn -oA tnet 10.129.2.18 10.129.2.19 10.129.2.20 | grep for | cut -d" " -f5
```
- **Results**:
    - Active hosts:
        - 10.129.2.18
        - 10.129.2.19
        - 10.129.2.20
- **Range Scanning**:
- If the IPs are contiguous, specify the range:
```
secmancer@htb[/htb]$ sudo nmap -sn -oA tnet 10.129.2.18-20 | grep for | cut -d" " -f5
```


#### Scan Single IP
- Before scanning a single host for open ports, check if it's alive:
- **Command**:
```
secmancer@htb[/htb]$ sudo nmap 10.129.2.18 -sn -oA host
```
- **Result**:
    - Host is up (0.087s latency).
    - MAC Address: DE:AD:00:00:BE
        
- **Scanning Options**:
    - `-sn`: Disables port scanning.
- **Using ICMP Echo Requests**: To ensure ICMP echo requests are sent:
```
secmancer@htb[/htb]$ sudo nmap 10.129.2.18 -sn -oA host -PE --packet-trace
```


### Additional Options
- To view reasons for the host status:
```
secmancer@htb[/htb]$ sudo nmap 10.129.2.18 -sn -oA host -PE --reason
```
- To disable ARP requests and force ICMP echo requests:
```
secmancer@htb[/htb]$ sudo nmap 10.129.2.18 -sn -oA host -PE --packet-trace --disable-arp-ping
```

### Resources
- For more strategies on host discovery, visit: [Nmap Host Discovery Strategies](https://nmap.org/book/host-discovery-strategies.html)

## Questions
- Based on the last result, find out which operating system it belongs to. Submit the name of the operating system as result.
	- Windows
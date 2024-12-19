### Introduction
- **Firewalls** control and monitor network traffic between different segments (internal, external, etc.), protecting networks from unauthorized access and security threats.
- **Linux** provides built-in firewall capabilities to filter incoming and outgoing traffic, preventing unauthorized access and mitigating security threats using rules based on protocols, ports, and other criteria.
- The goal of a firewall implementation varies depending on the needs of the organization, such as ensuring **confidentiality**, **integrity**, and **availability** of network resources.
- **iptables**, introduced in the Linux 2.4 kernel in 2000, replaced older tools like **ipchains** and **ipfwadm** and became the standard Linux firewall tool.
- **iptables** offers a flexible, command-line interface for filtering traffic based on various criteria (IP addresses, ports, protocols) and is highly customizable for complex rulesets to protect against security threats.
- **Netfilter**, integrated into the Linux kernel, is used to implement firewall functionality and provides hooks for modifying network traffic, with **iptables** used to configure firewall rules.



### Iptables
- **iptables** provides a flexible set of rules for filtering network traffic based on criteria like IP addresses, port numbers, and protocols. Other alternatives include **nftables**, **UFW**, and **FirewallD**.
- **nftables** offers a modern syntax and better performance compared to iptables, but migration requires effort as the syntax is not compatible.
- **UFW** (Uncomplicated Firewall) offers a user-friendly interface for configuring firewall rules, built on top of iptables and nftables.
- **FirewallD** is a dynamic and flexible firewall solution that supports complex configurations, custom firewall zones, and services, providing a rich set of rules for filtering network traffic.
![[Screenshot_20241108_202511.png]]



### Tables
- When working with firewalls on Linux systems, it is important to understand how tables work in iptables. 
- Tables in iptables are used to categorize and organize firewall rules based on the type of traffic that they are designed to handle. 
- These tables are used to organize and categorize firewall rules. 
- Each table is responsible for performing a specific set of tasks.
![[Screenshot_20241108_202534.png]]
- In addition to the built-in tables, iptables provides a fourth table called the raw table, which is used to configure special packet processing options. 
- The raw table contains two built-in chains: PREROUTING and OUTPUT.



### Chains
- In iptables, chains organize rules that define how network traffic should be filtered or modified. There are two types of chains in iptables:
	- Built-in chains
	- User-defined chains
- The built-in chains are pre-defined and automatically created when a table is created. Each table has a different set of built-in chains. For example, the filter table has three built-in chains:
	- INPUT
	- OUTPUT
	- FORWARD
- These chains are used to filter incoming and outgoing network traffic, as well as traffic that is being forwarded between different network interfaces. The nat table has two built-in chains:
	- PREROUTING
	- POSTROUTING
- The PREROUTING chain is used to modify the destination IP address of incoming packets before the routing table processes them. The POSTROUTING chain is used to modify the source IP address of outgoing packets after the routing table has processed them. The mangle table has five built-in chains:
	- PREROUTING
	- OUTPUT
	- INPUT
	- FORWARD
	- POSTROUTING
- These chains are used to modify the header fields of incoming and outgoing packets and packets being processed by the corresponding chains.
- `User-defined chains` can simplify rule management by grouping firewall rules based on specific criteria, such as source IP address, destination port, or protocol. 
- They can be added to any of the three main tables. 
- For example, if an organization has multiple web servers that all require similar firewall rules, the rules for each server could be grouped in a user-defined chain. 
- Another example is when a user-defined chain could filter traffic destined for a specific port, such as port 80 (HTTP). 
- The user could then add rules to this chain that specifically filter traffic destined for port 80.



### Rules and Targets
- Iptables rules are used to define the criteria for filtering network traffic and the actions to take for packets that match the criteria. 
- Rules are added to chains using the `-A` option followed by the chain name, and they can be modified or deleted using various other options.
- Each rule consists of a set of criteria or matches and a target specifying the action for packets that match the criteria. 
- The criteria or matches match specific fields in the IP header, such as the source or destination IP address, protocol, source, destination port number, and more. 
- The target specifies the action for packets that match the criteria. 
- They specify the action to take for packets that match a specific rule. 
- For example, targets can accept, drop, reject, or modify the packets. 
- Some of the common targets used in iptables rules include the following.
![[Screenshot_20241108_202825.png]]
- Let us illustrate a rule and consider that we want to add a new entry to the INPUT chain that allows incoming TCP traffic on port 22 (SSH) to be accepted. 
- The command for that would look like the following.
```shell-session
secmancer@htb[/htb]$ sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```



### Matches
- `Matches` are used to specify the criteria that determine whether a firewall rule should be applied to a particular packet or connection.
- Matches are used to match specific characteristics of network traffic, such as the source or destination IP address, protocol, port number, and more.
![[Screenshot_20241108_202854.png]]
- In general, matches are specified using the '-m' option in iptables. 
- For example, the following command adds a rule to the 'INPUT' chain in the 'filter' table that matches incoming TCP traffic on port 80:
```shell-session
secmancer@htb[/htb]$ sudo iptables -A INPUT -p tcp -m tcp --dport 80 -j ACCEPT
```
- This example rule matches incoming TCP traffic (`-p tcp`) on port 80 (`--dport 80`) and jumps to the accept target (`-j ACCEPT`) if the match is successful.
![[Screenshot_20241108_202936.png]]

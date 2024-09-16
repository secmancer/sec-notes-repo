#### **Primary Goal of Firewalls**
- **Purpose**: Control and monitor network traffic between different network segments (e.g., internal and external networks or network zones).
- **Protection**: Shield computer networks from unauthorized access, malicious traffic, and other security threats.
- **Functionality**: Filter incoming and outgoing traffic based on pre-defined rules, protocols, ports, and other criteria to prevent unauthorized access and mitigate security threats.
- **Objective**: Varies based on organizational needs, including ensuring the confidentiality, integrity, and availability of network resources.

#### **Historical Context**
- **iptables**:
    - **Introduction**: Replaced earlier tools like `ipchains` and `ipfwadm`.
    - **First Introduced**: Linux 2.4 kernel in 2000.
    - **Significance**: Became the standard firewall solution for Linux systems.
    - **Features**:
        - **Command-Line Interface**: Provides a powerful and flexible interface for configuring firewall rules.
        - **Customizability**: Allows creation of complex firewall rulesets.
        - **Protection**: Guards against threats such as denial-of-service (DoS) attacks, port scans, and network intrusions.

#### **Firewall Implementation in Linux**
- **Netfilter Framework**:
    - **Integration**: Part of the Linux kernel.
    - **Functionality**: Provides hooks to intercept and modify network traffic as it passes through the system.
    - **Usage**: Configured via `iptables` to set firewall rules.

#### **Key Points**
- **Filtering Criteria**: IP addresses, ports, protocols, etc.
- **Role**: Ensures secure network communication by applying rules to manage traffic.
- **Tool Evolution**: `iptables` has evolved to become a core component of Linux network security, offering robust and flexible firewall capabilities.


#### **Key Features of Iptables**
- **Flexibility**: Filters network traffic based on source and destination IP addresses, port numbers, protocols, and other criteria.
- **Customization**: Allows for detailed and complex rule sets to control network access.

#### **Alternative Firewall Solutions**
1. **nftables**:
    - **Modern Syntax**: Provides a more modern syntax compared to iptables.
    - **Performance**: Offers improved performance over iptables.
    - **Compatibility**: Syntax is not compatible with iptables, requiring effort to migrate from iptables to nftables.
2. **UFW (Uncomplicated Firewall)**:
    - **Ease of Use**: Provides a simpler, user-friendly interface for configuring firewall rules.
    - **Framework**: Built on top of the iptables framework.
    - **Purpose**: Designed to make firewall management easier, especially for users who prefer not to use command-line tools.
3. **FirewallD**:
    - **Dynamic Configuration**: Offers a dynamic and flexible firewall solution.
    - **Custom Zones**: Supports creating custom firewall zones and services.
    - **Components**: Includes various components that work together to manage complex firewall configurations.

#### **Components of Iptables**
The main components of iptables include:
- **Tables**: Organizational structures that contain chains of rules.
    - **Filter Table**: Default table used for general filtering rules.
    - **NAT Table**: Used for network address translation rules.
    - **Mangle Table**: Used for specialized packet alteration.
    - **Raw Table**: Used for exemptions from connection tracking.
- **Chains**: Lists of rules within tables.
    - **INPUT Chain**: Handles incoming traffic.
    - **OUTPUT Chain**: Handles outgoing traffic.
    - **FORWARD Chain**: Handles traffic being routed through the system.
- **Rules**: Specific criteria within chains to match traffic and define actions (e.g., ACCEPT, DROP).

**Note**: Each alternative solution offers different features and capabilities, and the choice of which to use may depend on specific requirements and preferences.

![[Screenshot_20240912_145046.png]]

### Iptables Tables
**Tables** in iptables are used to organize and categorize firewall rules based on the type of traffic they handle. Each table is responsible for different tasks related to network traffic processing.

#### **Tables and Their Functions**
1. **Filter Table**
    - **Description**: Used to filter network traffic based on IP addresses, ports, and protocols.
    - **Built-in Chains**:
        - **INPUT**: Handles incoming traffic to the local system.
        - **OUTPUT**: Manages outgoing traffic from the local system.
        - **FORWARD**: Controls traffic being routed through the system.
2. **NAT Table**
    - **Description**: Used to modify the source or destination IP addresses of network packets.
    - **Built-in Chains**:
        - **PREROUTING**: Alters packets as they arrive, before routing decisions are made.
        - **POSTROUTING**: Alters packets after routing decisions have been made.
3. **Mangle Table**
    - **Description**: Used to modify the header fields of network packets.
    - **Built-in Chains**:
        - **PREROUTING**: Modifies packets before routing.
        - **OUTPUT**: Modifies packets as they are about to be sent out.
        - **INPUT**: Modifies packets as they arrive at the local system.
        - **FORWARD**: Modifies packets being routed through the system.
        - **POSTROUTING**: Modifies packets after routing decisions.
4. **Raw Table**
    - **Description**: Configures special packet processing options and exemptions from connection tracking.
    - **Built-in Chains**:
        - **PREROUTING**: Handles packets before routing.
        - **OUTPUT**: Handles packets as they are about to be sent out.

**Note**: Understanding the purpose of each table and its associated chains is crucial for effectively managing and configuring firewall rules with iptables.

![[Screenshot_20240912_145040.png]]

#### Chains

In iptables, chains organize rules that define how network traffic should be filtered or modified. There are two types of chains in iptables:
- Built-in chains
- User-defined chains

The built-in chains are pre-defined and automatically created when a table is created. Each table has a different set of built-in chains. For example, the filter table has three built-in chains:
- INPUT
- OUTPUT
- FORWARD

These chains are used to filter incoming and outgoing network traffic, as well as traffic that is being forwarded between different network interfaces. The nat table has two built-in chains:
- PREROUTING
- POSTROUTING

The PREROUTING chain is used to modify the destination IP address of incoming packets before the routing table processes them. The POSTROUTING chain is used to modify the source IP address of outgoing packets after the routing table has processed them. The mangle table has five built-in chains:
- PREROUTING
- OUTPUT
- INPUT
- FORWARD
- POSTROUTING

These chains are used to modify the header fields of incoming and outgoing packets and packets being processed by the corresponding chains.

`User-defined chains` can simplify rule management by grouping firewall rules based on specific criteria, such as source IP address, destination port, or protocol. They can be added to any of the three main tables. For example, if an organization has multiple web servers that all require similar firewall rules, the rules for each server could be grouped in a user-defined chain. Another example is when a user-defined chain could filter traffic destined for a specific port, such as port 80 (HTTP). The user could then add rules to this chain that specifically filter traffic destined for port 80.

#### Rules and Targets

Iptables rules are used to define the criteria for filtering network traffic and the actions to take for packets that match the criteria. Rules are added to chains using the `-A` option followed by the chain name, and they can be modified or deleted using various other options.

Each rule consists of a set of criteria or matches and a target specifying the action for packets that match the criteria. The criteria or matches match specific fields in the IP header, such as the source or destination IP address, protocol, source, destination port number, and more. The target specifies the action for packets that match the criteria. They specify the action to take for packets that match a specific rule. For example, targets can accept, drop, reject, or modify the packets. Some of the common targets used in iptables rules include the following:

|**Target Name**|**Description**|
|---|---|
|`ACCEPT`|Allows the packet to pass through the firewall and continue to its destination|
|`DROP`|Drops the packet, effectively blocking it from passing through the firewall|
|`REJECT`|Drops the packet and sends an error message back to the source address, notifying them that the packet was blocked|
|`LOG`|Logs the packet information to the system log|
|`SNAT`|Modifies the source IP address of the packet, typically used for Network Address Translation (NAT) to translate private IP addresses to public IP addresses|
|`DNAT`|Modifies the destination IP address of the packet, typically used for NAT to forward traffic from one IP address to another|
|`MASQUERADE`|Similar to SNAT but used when the source IP address is not fixed, such as in a dynamic IP address scenario|
|`REDIRECT`|Redirects packets to another port or IP address|
|`MARK`|Adds or modifies the Netfilter mark value of the packet, which can be used for advanced routing or other purposes|

![[Screenshot_20240912_145029.png]]

Let us illustrate a rule and consider that we want to add a new entry to the INPUT chain that allows incoming TCP traffic on port 22 (SSH) to be accepted. The command for that would look like the following:

Firewall Setup
```shell-session
secmancer@htb[/htb]$ sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

### Iptables Matches
**Matches** are used to specify criteria for applying firewall rules to network traffic. They define the characteristics that a packet or connection must have to match a rule. Here are some common match options:

- **`-p` or `--protocol`**: Matches the protocol (e.g., `tcp`, `udp`, `icmp`).
- **`--dport`**: Matches the destination port.
- **`--sport`**: Matches the source port.
- **`-s` or `--source`**: Matches the source IP address.
- **`-d` or `--destination`**: Matches the destination IP address.
- **`-m state`**: Matches the connection state (e.g., `NEW`, `ESTABLISHED`, `RELATED`).
- **`-m multiport`**: Matches multiple ports or port ranges.
- **`-m tcp`**: Matches TCP packets with additional TCP-specific options.
- **`-m udp`**: Matches UDP packets with additional UDP-specific options.
- **`-m string`**: Matches packets containing a specific string.
- **`-m limit`**: Matches packets at a specified rate limit.
- **`-m conntrack`**: Matches packets based on connection tracking information.
- **`-m mark`**: Matches packets based on Netfilter mark value.
- **`-m mac`**: Matches packets based on MAC address.
- **`-m iprange`**: Matches packets based on a range of IP addresses.

![[Screenshot_20240912_145020.png]]

**Example Command**: To add a rule to the `INPUT` chain in the `filter` table that allows incoming TCP traffic on port 80, use:
```
sudo iptables -A INPUT -p tcp -m tcp --dport 80 -j ACCEPT
```
This rule matches incoming TCP traffic (`-p tcp`) on port 80 (`--dport 80`) and allows it (`-j ACCEPT`).


### Firewall Setup Tasks
1. **Block Incoming Traffic on TCP/8080 Port**
```
sudo iptables -A INPUT -p tcp --dport 8080 -j DROP
```
2. **Allow Incoming Traffic on TCP/8080 Port**
```
sudo iptables -A INPUT -p tcp --dport 8080 -j ACCEPT
```
3. **Block Traffic from a Specific IP Address**
```
sudo iptables -A INPUT -s [SPECIFIC_IP_ADDRESS] -j DROP
```
4. **Allow Traffic from a Specific IP Address**
```
sudo iptables -A INPUT -s [SPECIFIC_IP_ADDRESS] -j ACCEPT
```
5. **Block Traffic Based on Protocol**
```
sudo iptables -A INPUT -p [PROTOCOL] -j DROP
```
6. **Allow Traffic Based on Protocol**
```
sudo iptables -A INPUT -p [PROTOCOL] -j ACCEPT
```
7. **Create a New Chain**
```
sudo iptables -N [CHAIN_NAME]
```
8. **Forward Traffic to a Specific Chain**
```
sudo iptables -A INPUT -j [CHAIN_NAME]
```
9. **Delete a Specific Rule**
```
sudo iptables -D [CHAIN_NAME] [RULE_SPECIFICATION]
```
10. **List All Existing Rules**
```
sudo iptables -L
```

![[Screenshot_20240912_145013.png]]
### **1. Overview of Firewalls**
- Firewalls **filter network traffic** between different network segments.
- Help prevent **unauthorized access, malicious traffic, and cyber threats**.
- Linux provides **built-in firewall capabilities** using tools like:
    - **iptables** (legacy but widely used)
    - **nftables** (modern alternative)
    - **UFW (Uncomplicated Firewall)** (simplified interface)
    - **FirewallD** (dynamic and flexible)



### **2. Introduction to iptables**
- Uses the **Netfilter framework** to filter and control network traffic.
- Organizes firewall rules using:
    - **Tables** (Categorizes rules)
    - **Chains** (Groups rules for specific traffic types)
    - **Rules** (Defines filtering conditions)
    - **Matches** (Criteria for rule application)
    - **Targets** (Actions to apply on matching packets)
- #### **Comparison of Firewall Tools**

| Tool          | Features                                    |
| ------------- | ------------------------------------------- |
| **iptables**  | Traditional, rule-based, widely used        |
| **nftables**  | Modern replacement, better performance      |
| **UFW**       | Simplified iptables interface               |
| **FirewallD** | Dynamic firewall with zone-based management |



### **3. iptables Components**
- #### **Tables in iptables**

|Table|Purpose|Built-in Chains|
|---|---|---|
|**filter**|Filters network traffic|INPUT, OUTPUT, FORWARD|
|**nat**|Modifies source/destination IPs|PREROUTING, POSTROUTING|
|**mangle**|Modifies packet headers|PREROUTING, INPUT, FORWARD, OUTPUT, POSTROUTING|
|**raw**|Special packet processing|PREROUTING, OUTPUT|

- #### **Chains in iptables**
	- **Built-in Chains:**
	    - **INPUT** – Handles incoming packets.
	    - **OUTPUT** – Handles outgoing packets.
	    - **FORWARD** – Handles packets passing through the system.
	    - **PREROUTING** – Alters packets before routing.
	    - **POSTROUTING** – Alters packets after routing.
	- **User-Defined Chains:**
	    - Custom chains for specific traffic filtering.



### **4. Rules, Targets, and Matches**
- #### **Common Targets**

|Target|Description|
|---|---|
|**ACCEPT**|Allows packet to pass|
|**DROP**|Silently drops the packet|
|**REJECT**|Drops packet and notifies sender|
|**LOG**|Logs packet information|
|**SNAT**|Modifies source IP (for NAT)|
|**DNAT**|Modifies destination IP (for NAT)|
|**MASQUERADE**|SNAT for dynamic IPs|
|**REDIRECT**|Redirects packet to another port|

- #### **Example: Allow SSH Traffic**
```sh
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```
- #### **Common Matches**

|Match|Description|
|---|---|
|`-p`|Protocol match (tcp, udp, icmp)|
|`--dport`|Match destination port|
|`--sport`|Match source port|
|`-s`|Match source IP|
|`-d`|Match destination IP|
|`-m state`|Match connection state (NEW, ESTABLISHED)|

- #### **Example: Allow HTTP Traffic**
```sh
sudo iptables -A INPUT -p tcp -m tcp --dport 80 -j ACCEPT
```



### **5. Practical iptables Configuration**
- #### **Block Incoming Traffic on TCP/8080**
```sh
sudo iptables -A INPUT -p tcp --dport 8080 -j DROP
```
- #### **Allow Incoming Traffic on TCP/8080**
```sh
sudo iptables -D INPUT -p tcp --dport 8080 -j DROP
sudo iptables -A INPUT -p tcp --dport 8080 -j ACCEPT
```
- #### **Block Traffic from a Specific IP**
```sh
sudo iptables -A INPUT -s 192.168.1.100 -j DROP
```
- #### **Allow Traffic from a Specific IP**
```sh
sudo iptables -A INPUT -s 192.168.1.200 -j ACCEPT
```
- #### **Block All ICMP (Ping) Traffic**
```sh
sudo iptables -A INPUT -p icmp -j DROP
```
- #### **Allow Only UDP Traffic**
```sh
sudo iptables -A INPUT -p udp -j ACCEPT
sudo iptables -A INPUT -p tcp -j DROP
```
- #### **Create a New Chain**
```sh
sudo iptables -N CUSTOM_CHAIN
```
- #### **Forward Traffic to a Custom Chain**
```sh
sudo iptables -A INPUT -p tcp --dport 443 -j CUSTOM_CHAIN
```
- #### **Delete a Specific Rule**
```sh
sudo iptables -D INPUT -p tcp --dport 22 -j ACCEPT
```
- #### **List All Existing Rules**
```sh
sudo iptables -L -v -n
```



### **Key Takeaways**
- Firewalls **filter and control** network traffic to enhance security.  
-  **iptables** is a powerful tool for **Linux firewall configuration**.  
- Understanding **tables, chains, rules, and targets** is essential for **effective firewall management**.  
- Practical firewall setup includes **allowing/blocking traffic**, **creating chains**, and **managing NAT**
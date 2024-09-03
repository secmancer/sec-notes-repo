### 1. Block Incoming Traffic on TCP Port 8080

To block incoming traffic on port 8080: sudo iptables -A INPUT -p tcp --dport 8080 -j DROP

### 2. Allow Incoming Traffic on TCP Port 8080

To allow incoming traffic on port 8080: sudo iptables -A INPUT -p tcp --dport 8080 -j ACCEPT

### 3. Block Traffic from a Specific IP Address

To block traffic from IP address `192.168.1.100`: sudo iptables -A INPUT -s 192.168.1.100 -j DROP

### 4. Allow Traffic from a Specific IP Address

To allow traffic from IP address `192.168.1.100`: sudo iptables -A INPUT -s 192.168.1.100 -j ACCEPT

### 5. Block Traffic Based on Protocol

To block UDP traffic: sudo iptables -A INPUT -p udp -j DROP

### 6. Allow Traffic Based on Protocol

To allow TCP traffic: sudo iptables -A INPUT -p tcp -j ACCEPT

### 7. Create a New Chain

To create a new chain called `MYCHAIN` in the `filter` table: sudo iptables -N MYCHAIN

### 8. Forward Traffic to a Specific Chain

To forward traffic to `MYCHAIN` for incoming TCP traffic on port 80:
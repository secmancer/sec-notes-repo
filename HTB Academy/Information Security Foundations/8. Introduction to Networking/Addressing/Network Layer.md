### Network Layer (Layer 3) - OSI Model

**Functionality**:
- **Data Packet Exchange**: Controls how data packets are exchanged between nodes. Direct routing to the receiver is not always possible, so packets are transferred from node to node until reaching the destination.
- **Routing and Data Flow Control**: Responsible for setting up and clearing connection channels, routing data, and controlling data flow. Nodes process addresses to route packets through the network.

**Key Responsibilities**:
- **Logical Addressing**: Assigns and manages logical addresses for network devices.
- **Routing**: Determines the best path for data packets to travel across the network.

**Common Protocols**:
- **IPv4 / IPv6**: Protocols for addressing and routing data packets.
- **IPsec**: Provides security for IP communications.
- **ICMP (Internet Control Message Protocol)**: Handles error messages and operational information.
- **IGMP (Internet Group Management Protocol)**: Manages group memberships in multicast applications.
- **RIP (Routing Information Protocol)**: A distance-vector routing protocol.
- **OSPF (Open Shortest Path First)**: A link-state routing protocol.

**Operational Details**:
- **Routing Tables**: Nodes use routing tables to determine where to forward packets based on the addresses.
- **Inter-Subnet Communication**: Ensures packets are routed between subnets with potentially different or incompatible addressing schemes.
- **Forwarding Mechanism**: Packets are forwarded from node to node until they reach their destination. Intermediate nodes (routers) manage this process, and packets are assigned new destinations as they pass through the network.

**Note**:
- The network layer does not process data in higher layers; it primarily focuses on routing and addressing at Layer 3.
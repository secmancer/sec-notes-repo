### Network Topology
**Definition**: A network topology is the arrangement and connection of devices in a network, defining how components are laid out and how they interact.
1. **Connections**
    - **Wired Connections**:
        - **Coaxial Cabling**: Traditional cable used for internet and TV signals.
        - **Glass Fiber Cabling**: High-speed data transmission using light signals.
        - **Twisted-Pair Cabling**: Commonly used for Ethernet networks, with pairs of wires twisted together to reduce interference.
        - **Others**: Includes other types of physical connections like powerline networking.
    - **Wireless Connections**:
        - **Wi-Fi**: Wireless networking technology based on radio waves.
        - **Cellular**: Mobile networks such as 4G and 5G.
        - **Satellite**: Internet and communication via satellite signals.
        - **Others**: Includes other wireless technologies like Bluetooth.
2. **Nodes - Network Interface Controllers (NICs)**
    - **Repeaters**: Amplify signals to extend the range of a network.
    - **Hubs**: Basic networking device that connects multiple devices, broadcasting data to all ports.
    - **Bridges**: Connect and filter traffic between different network segments.
    - **Switches**: Direct data to specific devices on a network.
    - **Router/Modem**: Routes data between different networks (e.g., between a LAN and the Internet).
    - **Gateways**: Connect different network architectures or protocols.
    - **Firewalls**: Provide security by filtering traffic between networks.
    
**Note**: Network nodes are the connection points in the network where data is transmitted and received. They can be simple devices like microcontrollers or more complex devices with programmable capabilities.


3. **Classifications**
    - **Physical Topology**: The actual physical layout of the network devices and cabling.
    - **Logical Topology**: The logical flow of data and how it is transmitted across the network.



**Basic Network Topologies**:
1. **Point-to-Point**: A direct connection between two devices.
2. **Bus**: All devices share a single communication line.
3. **Star**: All devices connect to a central hub or switch.
4. **Ring**: Devices are connected in a circular fashion, with data traveling in one or both directions.
5. **Mesh**: Every device connects to every other device, providing multiple paths for data.
6. **Tree**: A hierarchical structure with a central root node and branching nodes.
7. **Hybrid**: Combination of two or more basic topologies to create a more complex network.
8. **Daisy Chain**: Devices are connected sequentially, forming a chain.



**Note**: While the physical arrangement of devices may differ, network topologies can be represented logically in various ways. For example, a LAN might be physically arranged in a circle but function logically as a star network.


### Point-to-Point Topology

**Definition**: The point-to-point topology is the simplest network configuration, consisting of a direct, dedicated connection between two hosts. This configuration facilitates straightforward and exclusive communication between these two devices.
**Characteristics**:
- **Direct Link**: A physical connection exists solely between two devices.
- **Exclusive Communication**: Only the two connected devices can communicate with each other.
- **Simple Setup**: Easy to implement due to its straightforward nature.
**Applications**:
- **Traditional Telephony**: Used in traditional telephone systems where each call is a direct connection between two telephones.
**Distinction**:
- **Not to be Confused with P2P**: Point-to-point topology should not be confused with P2P (Peer-to-Peer) architecture, which involves a decentralized network model where each device can act as both a client and a server.

![[topo_p2p.png]]


### Bus Topology
**Definition**: In a bus topology, all network hosts are connected to a single transmission medium. The medium can be a coaxial cable or another type of shared communication channel.

**Characteristics**:
- **Shared Medium**: All devices are connected to a common transmission medium.
- **No Central Control**: There is no central network component managing the communication processes.
- **Single Communication Path**: Only one device can transmit data at a time, while all others can only receive and process the data.

**Functionality**:
- **Data Transmission**: When a device sends data, it travels along the bus and can be received by all other devices connected to the same medium.
- **Addressing**: Each device on the bus must check the data to determine if it is intended for itself.

![[topo_bus.png]]



### Star Topology

**Definition**: In a star topology, all network hosts are connected to a central network component. This central component is usually a router, hub, or switch.

**Characteristics**:
- **Central Component**: All devices are connected to a central device that manages communication.
- **Separate Links**: Each host has a dedicated link to the central component.
- **Data Forwarding**: The central component handles the forwarding of data packets between hosts.

**Functionality**:
- **Data Transmission**: Data packets are received by the central component and then forwarded to the intended destination.
- **Traffic Load**: The central component can experience high data traffic, as it manages all connections and data exchanges.

![[topo_star.png]]



### Ring Topology

**Definition**: In a ring topology, each host or node is connected to two other nodes, forming a closed loop or ring.

**Physical Ring Topology**:
- **Connections**:
    - **Incoming Cable**: Receives signals from the previous node.
    - **Outgoing Cable**: Sends signals to the next node.
- **No Central Component**: Typically does not require a central network device.
- **Protocol-Based**: Control and access to the transmission medium are managed by a protocol that all stations adhere to.

**Logical Ring Topology**:
- **Implementation**: Often simulated using a physical star topology where a distributor at the node emulates the ring by forwarding data from one port to the next.

**Data Transmission**:
- **Direction**: Information is transmitted in a predetermined direction around the ring.
- **Access Method**:
    - **Sequential Access**: Data is passed from station to station.
    - **Token Passing**: A token, a bit pattern, continuously circulates through the network. The token-based access method controls the access to the network and ensures orderly data transmission.


![[topo_ring.png]]



### Mesh Topology
**Definition**: Mesh topology is a network structure where nodes are interconnected, allowing for multiple paths for data transmission. It does not adhere to a fixed topology, offering flexibility in connections and routing.

**Types of Mesh Topologies**:
1. **Fully Meshed Structure**:
    - **Connections**: Every node is directly connected to every other node in the network.
    - **Reliability**: Provides high reliability and redundancy. If one node fails, others continue to function, ensuring network resilience.
    - **Applications**: Commonly used in Wide Area Networks (WAN) or Metropolitan Area Networks (MAN) to enhance reliability and bandwidth.
    - **Routing**: Each node has routing functions and knowledge of neighboring nodes, which aids in efficient data transmission and traffic management.
2. **Partially Meshed Structure**:
    - **Connections**: Not all nodes are interconnected. Some nodes are connected to exactly one other node, while others may have multiple connections.
    - **Flexibility**: This topology provides a balance between full connectivity and simplicity, often used to optimize cost and network performance.

**Key Features**:
- **Data Transmission**: Multiple paths for data to travel, enhancing network resilience and minimizing the impact of node failures.
- **Routing**: Nodes in a fully meshed network have routing functions and awareness of their neighbors, while partially meshed networks have varied connectivity.

![[topo_mesh.png]]



### Tree Topology

**Definition**: Tree topology is an extension of the star topology, designed to accommodate larger and more complex network structures. It combines multiple star topologies in a hierarchical manner, making it suitable for extensive networks.

**Features**:
- **Structure**:
    - **Logical Tree**: Defined by spanning trees that manage the network's layout and prevent loops.
    - **Physical Tree**: Built on structured cabling with a hierarchy of hubs, switches, or routers.

**Applications**:
- **Large Networks**: Commonly used in larger buildings and extensive organizational networks to support scalability and organization.
- **Broadband and City Networks**: Applied in Metropolitan Area Networks (MAN) and broadband networks to manage large-scale connectivity.

**Key Aspects**:
- **Hierarchy**: Includes a central root node connected to multiple subordinate nodes, which in turn connect to other nodes, forming a tree-like structure.
- **Scalability**: Supports expansion by adding additional branches and nodes without disrupting the existing network.
- **Modular Design**: Allows for structured cabling and efficient network management.

![[topo_tree.png]]




### Hybrid Topology

**Definition**: Hybrid topology combines two or more different network topologies into a single network. This results in a network structure that does not conform to a standard single topology but instead integrates multiple topologies.

**Characteristics**:
- **Combination**: Integrates various basic topologies, such as star, bus, ring, and mesh, to form a hybrid structure.
- **Flexibility**: Adaptable to specific needs by combining the strengths of different topologies.

**Examples**:
- **Tree Network with Bus**: A network where star topologies are interconnected via a bus topology, forming a hybrid structure.
- **Interconnected Trees**: A scenario where multiple tree topologies are linked, but the overall network may still function as a tree topology.

**Key Points**:
- **Customization**: Allows for tailored network designs that can leverage the advantages of each integrated topology.
- **Scalability and Efficiency**: Provides the ability to design networks that meet complex organizational needs and optimize performance.

![[topo_hybrid.png]]



### Daisy Chain Topology

**Definition**: In daisy chain topology, multiple hosts or devices are connected in series, with each device linked to the next in a sequential manner.

**Characteristics**:
- **Connection**: Devices are connected one after another, forming a chain-like structure.
- **Series Configuration**: Similar to how multiple hardware components are linked in series, creating a daisy-chain configuration.

**Applications**:
- **Automation Technology**: Commonly used in automation networks, such as Controller Area Network (CAN) for industrial systems.

**Signal Transmission**:
- **Physical Arrangement**: Based on the physical layout where signals are transmitted through a series of nodes.
- **Data Flow**: Data is sent from one device to the next in the chain until it reaches the destination.

**Considerations**:
- **Single Path**: There is only one path for data transmission, which can create potential points of failure if any link in the chain is disrupted.
- **Latency**: Data has to pass through each device in the chain, which can introduce delays.


![[topo_daisy-chain.png]]
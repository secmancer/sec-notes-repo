### Networking Models: OSI and TCP/IP

![[net_models4 1.png]]
#### OSI Model
- **Definition**: The OSI (Open Systems Interconnection) model is a reference model used to describe and define communication between systems. It breaks down the communication process into seven distinct layers, each with specific functions.
    
- **Purpose**: Provides a framework for understanding and designing network systems and protocols. It is used to conceptualize the interactions between network components.
    
- **Layers**:
    1. **Physical Layer**: Manages the physical connection between devices, including cables and hardware.
    2. **Data Link Layer**: Handles error detection and correction, and manages the data frames between devices on the same network.
    3. **Network Layer**: Responsible for routing data packets between devices across different networks and managing logical addressing.
    4. **Transport Layer**: Ensures reliable data transfer between hosts, handling error recovery and flow control.
    5. **Session Layer**: Manages sessions and controls the dialog between two devices.
    6. **Presentation Layer**: Translates data formats between the application layer and the network, ensuring proper data representation and encryption.
    7. **Application Layer**: Provides network services directly to applications, such as file transfer, email, and network management.
- **Publication**: Developed by the International Telecommunication Union (ITU) and the International Organization for Standardization (ISO). It is sometimes referred to as the ISO/OSI layer model.
    

#### TCP/IP Model
- **Definition**: The TCP/IP (Transmission Control Protocol/Internet Protocol) model is a more practical and widely used networking model that simplifies the OSI model into four layers. It is the foundation of the internet and many other network protocols.
    
- **Purpose**: Provides a framework for network communication that is implemented in real-world networks, including the internet.
    
- **Layers**:
    1. **Network Interface Layer**: Corresponds to the OSI Physical and Data Link layers. It handles the physical connection and the protocol used to transmit data over a network.
    2. **Internet Layer**: Matches the OSI Network layer. It manages logical addressing and routing of data packets across networks.
    3. **Transport Layer**: Similar to the OSI Transport layer. It ensures reliable data transfer between hosts using protocols like TCP and UDP.
    4. **Application Layer**: Combines the OSI Session, Presentation, and Application layers. It provides network services directly to applications and handles data formatting and application-level protocols.
- **Focus**: More practical and closely aligned with real-world network implementations compared to the OSI model.

#### ISO/OSI vs. TCP/IP
- **TCP/IP Model**:
    - **Purpose**: Facilitates host connectivity to the Internet, using a flexible approach with fewer rigid rules compared to OSI.
    - **Structure**: Emphasizes practical implementation, aligning closely with real-world network operations.
    - **Protocols**: Includes various protocols like TCP and UDP for different functions, such as reliable data transfer and connectionless communication.
- **OSI Model**:
    - **Purpose**: Acts as a communication gateway between networks and end-users, providing a theoretical framework for network communication.
    - **Structure**: Known for its strict, structured approach and detailed protocol specifications.
    - **Usage**: Often used as a reference model for understanding and designing network systems.

#### Packet Transfers
- **Layered System**: In a network model, data is handled in layers, each with specific functions. The data moves through these layers as Protocol Data Units (PDUs).
    - **Application Layer**: The initial layer where application requests are processed.
    - **Data Processing**: As data passes through each layer, it is encapsulated with additional protocol information appropriate to that layer’s function.
    - **Physical Transfer**: Data reaches the physical layer for transmission over the network medium.
    - **Routing and Reassembly**: Data is routed through the network, with each layer performing its designated operations. Upon reaching the destination, the data is de-encapsulated and processed by the receiving application.

![[net_models_pdu2.png]]



### Encapsulation and Data Transmission Process

- **Encapsulation**:
    - **Definition**: The process where each layer of a network model adds a header to the Protocol Data Unit (PDU) from the layer above it. This header includes control and identification information.
    - **Process**:
        - The **header** and the **data** together form the PDU for the next layer.
        - Each layer encapsulates the data with its own header before passing it down to the next layer.
- **Transmission**:
    - **Layers Involved**: The data continues to be encapsulated as it moves through the layers until it reaches the Physical Layer or Network Layer for transmission.
    - **Physical Layer**: The encapsulated data is converted into signals or packets suitable for transmission over the network medium.
- **Reception**:
    - **Decapsulation**:
        - The receiver processes the data by reversing the encapsulation process.
        - Each layer removes the header added by the corresponding layer at the sender’s side and extracts the data.
    - **Data Utilization**: After all layers have removed their respective headers, the application layer receives and processes the final data.
- **Overall Process**:
    - **Sending Data**:
        - The data is encapsulated with headers at each layer.
        - It is transmitted through the network.
    - **Receiving Data**:
        - The data is decapsulated by removing headers at each layer.
        - The final data is used by the application at the receiving end.



![[packet_transfer.png]]


### Importance of OSI and TCP/IP Models for Penetration Testing

- **TCP/IP Model**:
    - **Usage**: Helps in understanding the overall connection establishment process.
    - **Benefits**: Provides a quick overview of how connections are established and how data is transmitted across the Internet.
    - **Application**: Useful for getting a general sense of network communication, especially in real-time scenarios.
- **OSI Model**:
    - **Usage**: Useful for detailed analysis and dissection of network traffic.
    - **Benefits**: Allows for in-depth analysis by breaking down the communication process into its seven layers.
    - **Application**: Ideal for examining and understanding specific layers of network traffic, which is crucial when intercepting and analyzing traffic.
- **Network Traffic Analysis**:
    - **Focus**: Involves listening to and intercepting network traffic for analysis.
    - **Tools and Techniques**: Requires familiarity with both reference models to effectively analyze traffic at various layers.
- **Familiarity with Both Models**:
    - **Recommendation**: Penetration testers should understand and internalize both the TCP/IP and OSI models.
    - **Reason**: Combining the general overview provided by TCP/IP with the detailed layer-by-layer analysis offered by OSI enhances the ability to perform effective network traffic analysis and security assessments.
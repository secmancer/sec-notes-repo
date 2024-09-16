### ISO/OSI Model Overview
**Objective**:
- **Goal**: Create a reference model for communication across different technical systems and technologies.
- **Purpose**: Ensure compatibility and trace the structure and establishment of connections.

![[Screenshot_20240916_113027.png]]


**Layers and Functions**:
1. **Application Layer (Layer 7)**:
    - **Function**: Controls data input and output and provides application-specific functions.
    - **Role**: Interfaces directly with user applications.
2. **Presentation Layer (Layer 6)**:
    - **Function**: Translates system-dependent data formats into a format independent of the application.
    - **Role**: Handles data encryption, compression, and translation.
3. **Session Layer (Layer 5)**:
    - **Function**: Manages logical connections between systems, handling session establishment, maintenance, and termination.
    - **Role**: Ensures session reliability and prevents connection issues.
4. **Transport Layer (Layer 4)**:
    - **Function**: Provides end-to-end control of data, ensuring reliable data transfer and handling flow control, segmentation, and reassembly.
    - **Role**: Manages data integrity and error correction.
5. **Network Layer (Layer 3)**:
    - **Function**: Establishes, maintains, and terminates connections in circuit-switched networks and forwards data packets in packet-switched networks.
    - **Role**: Handles routing and addressing.
6. **Data Link Layer (Layer 2)**:
    - **Function**: Ensures reliable and error-free transmission over the physical medium by dividing bitstreams into frames.
    - **Role**: Manages error detection and correction at the data link level.
7. **Physical Layer (Layer 1)**:
    - **Function**: Deals with the physical transmission of data using electrical, optical, or electromagnetic signals.
    - **Role**: Handles the actual data transmission over physical media.

**Layer Characteristics**:
- **Transport-Oriented Layers**: Layers 2-4 (Data Link, Network, Transport).
- **Application-Oriented Layers**: Layers 5-7 (Session, Presentation, Application).

**Data Transmission Process**:
- **Sending**: Data is processed from Layer 7 to Layer 1.
- **Receiving**: Data is unpacked from Layer 1 to Layer 7.

**Communication**:
- Both sender and receiver must process all seven layers, ensuring tasks at each layer are completed to maintain security, reliability, and performance.
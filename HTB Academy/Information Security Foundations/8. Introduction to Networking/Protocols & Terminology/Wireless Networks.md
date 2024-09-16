### Wireless Networks
- **Definition**: Wireless networks use wireless data connections between network nodes, allowing devices like laptops, smartphones, and tablets to communicate without physical cables.
    
- **Technology**:
    - Utilizes radio frequency (RF) technology to transmit data.
    - Devices have wireless adapters that convert data into RF signals for transmission and vice versa.
- **Types**:
    - **Local Area Network (LAN)**: Uses WiFi for small areas (e.g., home, office) with a range of a few hundred feet.
    - **Wide Area Network (WWAN)**: Uses cellular data technologies (3G, 4G LTE, 5G) for larger areas (e.g., cities, regions).
- **Connection**:
    - Devices must be within range and have correct network settings (network name and password) to connect.
    - Communication happens over RF in the 2.4 GHz or 5 GHz bands.
- **Access Point**:
    - **Wireless Access Point (WAP)**: Central device (e.g., router) that connects wireless to wired networks and controls access.
    - **Process**: Device requests permission from WAP to transmit data. WAP grants permission and manages the communication.
- **Signal Strength**:
    - Influenced by transmitter power, obstacles, and RF noise.
    - Techniques like spread spectrum transmission and error correction are used for reliability.

### WiFi Connection
- **Protocol**: IEEE 802.11 defines how devices communicate over WiFi.
    - **Connection Request Frame**:
        - **MAC Address**: Unique identifier for the device.
        - **SSID**: Network name.
        - **Supported Data Rates**: Data rates device can handle.
        - **Supported Channels**: Channels device can communicate on.
        - **Supported Security Protocols**: Security methods device supports (e.g., WPA2/WPA3).
- **Hidden SSID**:
    - SSID can be hidden by disabling broadcasting.
    - Still detectable in authentication packets.
- **Additional Protocols**:
    - **TCP/IP**: For IP address assignment and routing.
    - **DHCP**: For dynamic IP address assignment.
    - **WPA2/WPA3**: For network security.

### WEP Challenge-Response Handshake
- **Process**:
    1. **Client**: Sends association request to WAP.
    2. **WAP**: Sends association response with a challenge string.
    3. **Client**: Calculates response and sends it back.
    4. **WAP**: Verifies response and sends authentication response.
- **CRC Checksum**:
    - Ensures data integrity by verifying packet data.
    - CRC value can reveal plaintext data due to its use on plaintext, not encrypted data.

### Security Features
- **Encryption**:
    - **WEP**: Uses 40-bit or 104-bit keys. Vulnerable to attacks and generally considered insecure.
    - **WPA/WPA2**: Uses stronger encryption (e.g., AES). WPA2 is more secure than WEP.
    - **WPA3**: Latest and most secure.
- **Access Control**:
    - Requires passwords or unique identifiers (MAC addresses) to join the network.
- **Firewall**:
    - Controls incoming and outgoing network traffic based on security rules.

### Encryption Protocols
- **WEP**:
    - Uses RC4 cipher and has two versions: WEP-40 (40-bit key) and WEP-104 (104-bit key).
    - **IV**: Initialization Vector included in packet headers (24-bit for both versions).
- **WPA**:
    - Provides higher security than WEP.
    - **WPA-Personal**: For small networks.
    - **WPA-Enterprise**: For larger organizations with centralized authentication.

### Authentication Protocols
- **LEAP**:
    - Uses a shared key for authentication, which is less secure.
- **PEAP**:
    - Uses tunneled TLS for secure authentication with digital certificates.
- **TACACS+**:
    - Used for authenticating users accessing network devices.
    - Authentication request may be encrypted (e.g., SSL/TLS or IPSec).

### Disassociation Attack
- **Definition**:
    - Disrupts communication between WAP and clients by sending disassociation frames.
    - Causes clients to disconnect and possibly reconnect, which can be used as a precursor to further attacks.

### Wireless Hardening
- **Disabling Broadcasting**:
    - Hides SSID from being broadcasted, making it less visible.
- **WPA**:
    - Provides strong encryption and authentication.
    - **WPA-Personal**: For home/small business networks.
    - **WPA-Enterprise**: For larger organizations with centralized authentication.
- **MAC Filtering**:
    - Accepts or rejects connections based on MAC addresses.
- **Deploying EAP-TLS**:
    - Uses digital certificates and PKI for strong authentication and encryption.
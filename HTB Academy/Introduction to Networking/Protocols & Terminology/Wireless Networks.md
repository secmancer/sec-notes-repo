### **Wireless Networks Overview**

- **Definition:** Networks that use wireless data connections to allow devices to communicate without physical cables.
- **Technology:** Utilizes radio frequency (RF) signals. Devices have wireless adapters that convert data into RF signals for transmission and reception.
- **Types:**
    - **WiFi (Local Area Network - LAN):** Covers small areas (e.g., homes, offices) with ranges up to a few hundred feet.
    - **Cellular Data (Wide Area Network - WWAN):** Uses technologies like 3G, 4G LTE, 5G, covering larger areas such as cities or regions.

### **WiFi Network Connection**

- **Connection Process:**
    
    1. Device sends a connection request frame to the Wireless Access Point (WAP).
    2. WAP responds with a challenge string.
    3. Device calculates a response and sends it back.
    4. WAP verifies the response and completes the connection.
- **IEEE 802.11 Protocol:**
    
    - Handles how devices communicate with WAPs.
    - Connection request frame includes:
        - MAC Address
        - SSID (Network Name)
        - Supported Data Rates and Channels
        - Supported Security Protocols

### **Security Protocols**

- **WEP (Wired Equivalent Privacy):**
    
    - Uses 40-bit or 104-bit keys.
    - Vulnerable due to short Initialization Vector (IV) and flaws in encryption.
    - Divided into WEP-40/WEP-64 and WEP-104 with different key lengths.
- **WPA (WiFi Protected Access):**
    
    - Uses stronger encryption (e.g., AES) and authentication.
    - Two versions: WPA-Personal (for home networks) and WPA-Enterprise (for larger organizations with centralized authentication).
- **WPA3:**
    
    - Provides enhanced security features compared to WPA2.

### **Authentication Protocols**

- **LEAP (Lightweight Extensible Authentication Protocol):**
    
    - Uses a shared key for authentication.
- **PEAP (Protected Extensible Authentication Protocol):**
    
    - Utilizes tunneled TLS for secure authentication with digital certificates.
- **TACACS+:**
    
    - Used for authenticating and authorizing network devices.
    - Requests are typically encrypted using methods like SSL/TLS or IPSec.

### **Disassociation Attack**

- **Description:**
    - Disrupts communication by sending disassociation frames to clients.
    - Forces clients to reconnect, potentially exposing them to further attacks.

### **Wireless Hardening Techniques**

- **Disabling SSID Broadcasting:**
    
    - Hides the network name to reduce visibility to unauthorized users.
- **WPA/WPA2/WPA3 Encryption:**
    
    - Provides strong encryption to secure data transmission.
- **MAC Filtering:**
    
    - Allows only devices with approved MAC addresses to connect.
- **Deploying EAP-TLS:**
    
    - Uses digital certificates for secure authentication and encryption.

### **Error Detection**

- **CRC (Cyclic Redundancy Check):**
    - Ensures data integrity by detecting errors in transmitted packets.
    - CRC values are recalculated and compared to detect data corruption.
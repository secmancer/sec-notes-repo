#### **Overview**
- **Network Traffic Analysis (NTA)** involves examining network data to determine its origin, impact, and to identify any deviations from normal behavior.
- **Objective:** Break down traffic into understandable segments, identify anomalies, potential malicious traffic, and compare against typical traffic baselines.



#### **Importance of Traffic Analysis**
- **Visibility:** Essential for detecting and responding to issues. Provides insight into network usage, top hosts and servers, and internal communications.
- **Baseline Setting:** Helps in establishing a baseline for normal network traffic, making it easier to detect anomalies or changes.
- **Advanced Implementations:** Incorporates tools like IDS/IPS, firewalls, and logs, integrated with platforms like Splunk or ELK Stack to enhance detection and response.




#### **Daily Operations**
- **Troubleshooting:** Live monitoring of network traffic helps resolve connection issues and verify protocol functionality.
- **Human Oversight:** Automated tools are useful but should be complemented with manual checks. The human eye is crucial for detecting sophisticated threats that may bypass automated systems.



#### **Traffic Capture Methods**
1. **Passive Capture:**
    - **Description:** Copying data without interacting with the packets directly.
    - **Dependencies:**
        - **Permission:** Required to capture data legally and ethically.
        - **Mirrored Port:** Network interface configured to copy traffic to a specific port.
        - **Capture Tool:** Requires tools like TCPDump or Wireshark.
        - **Storage and Processing Power:** Needs sufficient resources to handle large data volumes.
2. **Active Capture:**
    - **Description:** Involves direct interaction with the traffic, often in-line with the network.
    - **Dependencies:**
        - **Permission:** Same as passive capture.
        - **In-line Placement:** Requires network topology changes to capture traffic directly.
        - **Network Tap or Host With Multiple NICs:** Needed to handle and inspect traffic.
        - **Storage and Processing Power:** Similar requirements as passive capture, but potentially more intensive due to increased traffic.




#### **Understanding Baselines**
- **Importance:** Essential for distinguishing between normal and anomalous traffic.
- **Scenario Example:** Without a baseline, analyzing captured data from a network segment with connectivity issues can be overwhelming and time-consuming.
- **With Baseline:** Enables quick identification of anomalies by filtering out known-good traffic and focusing on deviations.



#### **Tools and Techniques**
- **Wireshark Modules:** Use tools like the top talkers' module to identify unusual traffic patterns.
- **Data Analysis:** Look for unusual connections and traffic patterns, such as unexpected ports or communication between unexpected hosts.
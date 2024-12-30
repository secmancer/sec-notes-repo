### Overview
- **Definition**: A DDoS attack disrupts the normal functioning of a website, server, or service by overwhelming it with a flood of internet traffic.
	- Unlike a traditional Denial of Service (DoS) attack, DDoS originates from multiple sources simultaneously.
	- Sources are often compromised devices (botnet) infected with malware.



### Analogy
- **Scenario**: A bakery hosting a grand opening is overwhelmed by a disruptive crowd, blocking real customers.
	- **In digital terms**: The overwhelming crowd = botnet; bakery = targeted website/service.
	- Result: The bakery’s operations are paralyzed, similar to a DDoS attack overwhelming a server.



### Key Elements
- **The Attacker**: Orchestrates the attack with the aim of disrupting the target.
- **The Botnet (Amplification Network)**:
    - Network of compromised devices, including personal computers, servers, and IoT devices (e.g., smart thermostats, cameras).
    - Devices are often hijacked without the owner's knowledge.
- **The Victim**: The targeted server, service, or network.



### Process
- The attacker sends commands to the botnet.
- Compromised devices in the botnet simultaneously send requests to the victim.
- Result:
    - The target’s bandwidth and processing capacity are overwhelmed.
    - Legitimate users experience delays or are unable to access the service.
    - Service slows down or crashes entirely.
- #### Example Scenario:
	- A small shop is flooded with an unexpected crowd (botnet) making normal operations impossible, paralyzing workflow.



### Impact
- **Case Study**:
    - **Dyn (2016)**: A major DDoS attack using the Mirai botnet.
        - Targeted IoT devices like cameras and routers.
        - Affected major websites (Twitter, Netflix, Reddit, etc.).
        - Millions of users and businesses experienced outages across the U.S. and Europe.
- **Consequences**:
    - **Financial Loss**: Downtime leads to lost sales/revenue for e-commerce sites, banks, streaming platforms, etc.
    - **Reputational Damage**:
        - Service outages erode customer trust.
        - Frequent issues may drive users to competitors.
    - **Operational Disruptions**:
        - Interrupts essential services, affecting not only the target but also dependent users.
    - **Security Risks**:
        - DDoS can act as a diversion while attackers exploit vulnerabilities to:
            - Breach data.
            - Install malware.
            - Execute further security breaches unnoticed.
### Importance of IT and Security Risks:
- IT is integral to nearly every company, with growing critical data and reliance on systems.
- Attacks like ransomware, data breaches, and system disruptions are common threats.
- Stolen or leaked data can be sold, used against companies, or exposed publicly.
- System failures, sometimes deliberate, are hard to counteract.

### Penetration Testing (Pentest):
- A **Pentest** is a structured, authorized attempt to test IT infrastructure by simulating real-world attacks.
- Pentesters aim to identify all vulnerabilities and assess their impact on **confidentiality, integrity, and availability** of systems.
- Unlike **vulnerability assessments**, pentests involve both manual and automated methods and are tailored to specific systems.
- **Objective**: To uncover vulnerabilities and improve system security. The client is responsible for fixing them.

### Risk Management:
- **Goal**: To identify, evaluate, and mitigate risks to an acceptable level, covering **confidentiality, integrity, and availability**.
- Methods include:
  - **Preventive measures** to reduce risk likelihood.
  - **Transferring risk** via insurance or third-party contracts.
  - **Mitigating impacts** of occurring risks.
- **Inherent risk**: Some risks remain even after proper controls are in place.

### Pentesting vs. Vulnerability Assessment:
- **Vulnerability assessment** uses automated tools to check known issues but lacks the adaptability of manual tests.
- **Pentests** involve detailed manual steps and require **explicit authorization** to avoid legal issues.
- Example: AWS doesn’t always need prior approval for some services.

### Pentesting Documentation:
- Pentesters provide detailed documentation of findings and recommendations, but clients are responsible for implementing fixes.
- A pentest provides a **snapshot** of security at a given moment, not ongoing monitoring.

### Testing Perspectives:
- **External** Pentests: Performed from outside the network, aiming to breach external defenses (e.g., through a VPN or VPS).
- **Internal** Pentests: Performed inside the network, often following successful external breaches or assumed breach scenarios.

### Types of Pentests:
1. **Blackbox**: Minimal information provided (IP addresses, domains).
2. **Greybox**: Extended information (URLs, hostnames, subnets).
3. **Whitebox**: Full internal information (configurations, credentials).
4. **Red-Teaming**: Simulates real-world attacks, may include physical testing and social engineering.
5. **Purple-Teaming**: Collaboration between pentesters and defenders.

### Testing Environments:
- Pentests cover a range of environments including:
  - **Network, Web App, Mobile, API, IoT**
  - **Cloud, Source Code, Physical Security, Hosts, Servers**
  - **Security Policies, Firewalls, IDS/IPS**
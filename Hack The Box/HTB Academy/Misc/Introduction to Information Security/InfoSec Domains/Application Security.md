### Overview
- Vital aspect of InfoSec
- Aims to protect software applications from external threats throughout their lifecycle
- Ensures the CIA triad of data/systems



### Key Concepts
- Secure Development Practices:
	- Secure Authentication: Implement strong locks on entry points (e.g., login mechanisms).
	- Write Secure Code: Avoid vulnerabilities like SQL injection, XSS, and buffer overflows.
	- Encrypt Data: Protect sensitive information in transit and at rest.
- Vulnerability Testing:
	- Conduct penetration testing to simulate attacks and find weaknesses.
	- Identify bugs or weak spots in the code.
	- Test for data security under various conditions.
- Ongoing Security Monitoring
	- Monitor for new threats and anomalies.
	- Apply updates and patches to address vulnerabilities.
- Security by Design:
	- Incorporate security from the start of development.
	- Use threat modeling to anticipate risks.
	- Conduct secure code reviews to identify potential issues.
	- Secure servers, databases, and environments supporting the application.



### Pseudocode
```
# 1. Start Building the House (Develop the App)
def build_house():
    install_locks_on_doors_and_windows()  # Secure Authentication
    use_strong_materials_for_walls()     # Write Secure Code
    install_waterproof_roof()            # Encrypt Data

# 2. Inspect the House for Weak Spots (Test for Vulnerabilities)
def inspect_house():
    test_if_locks_are_working()          # Penetration Testing
    look_for_cracks_in_walls()           # Check for Bugs
    test_roof_with_water()               # Test Data Security

# 3. Keep the House Safe Over Time (Ongoing Security Monitoring)
def maintain_house_security():
    install_security_cameras()           # Monitor for Threats
    repair_cracks_and_replace_broken_locks()  # Patch Vulnerabilities

# Overall Application Security Process
def protect_application():
    build_house()
    inspect_house()
    maintain_house_security()

# Execute security process
protect_application()
```



### Responsibilities
1. **Developers:** Write secure code and follow security best practices.
2. **Security Architects:** Design overall application and infrastructure security.
3. **IT Operations:** Maintain the security of production environments.
4. **Application Security Manager/CISO:** Set policies, ensure compliance, and oversee security implementations.



### Secure Testing
- Static and Dynamic Analysis Tools: Identify vulnerabilities in the code.
- Fuzzing Techniques: Test app resilience against unexpected inputs.
- Simulated Attacks: Assess the application’s defenses in real-world scenarios.
- Ongoing Monitoring: Use automated tools and regular assessments to keep security measures up-to-date.



### Obstacles
- Balancing security and speed: Tight deadlines often lead to rushed security checks, leaving vulnerabilities.
- The evolving threat landscape requires constant vigilance and updates.



### Questions
- What does the "C" in the CIA triad stand for?
	- confidentiality
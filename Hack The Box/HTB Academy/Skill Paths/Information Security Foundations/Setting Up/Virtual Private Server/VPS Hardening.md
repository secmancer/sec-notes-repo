### **Purpose of VPS Hardening**
- Reduce the attack surface by disabling unnecessary services and ports.
- Secure SSH access as the sole entry point.
- Protect sensitive data and ensure minimal exposure.



### **Key Steps for VPS Hardening**
- #### **1. Update the System**
	- Keep the VPS software up-to-date to minimize vulnerabilities.
```bash
sudo apt update -y && sudo apt full-upgrade -y && sudo apt autoremove -y && sudo apt autoclean -y
```
- #### **2. Install and Configure Fail2Ban**
	- **Fail2Ban** protects against brute-force attacks by banning IPs after repeated failed login attempts.
1. **Install Fail2Ban**:
    ```bash
    sudo apt install fail2ban -y
    ```
2. **Backup Configuration**:
    ```bash
    sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.conf.bak
    ```
3. **Enable SSH Monitoring**: Edit `/etc/fail2ban/jail.conf`:
    ```bash
    [sshd]
    enabled = true
    bantime = 4w
    maxretry = 3
    ```
- #### **3. Harden SSH Configuration**
	- Edit `/etc/ssh/sshd_config` to enhance SSH security:
1. **Backup SSH Configuration**:
    ```bash
    sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
    ```
2. **Recommended Settings**:
    ```plaintext
    LogLevel VERBOSE
    PermitRootLogin no
    MaxAuthTries 3
    MaxSessions 5
    HostbasedAuthentication no
    PermitEmptyPasswords no
    X11Forwarding no
    PrintMotd no
    ClientAliveInterval 600
    ClientAliveCountMax 0
    AllowUsers <username>
    Protocol 2
    AuthenticationMethods publickey,keyboard-interactive
    PasswordAuthentication no
    ```
3. **Restart SSH Service**:
    ```bash
    sudo service ssh restart
    ```



### **4. Enable Two-Factor Authentication (2FA)**
- **2FA** adds an additional layer of security by requiring a one-time password (OTP) in addition to the SSH key.
1. **Install Google Authenticator PAM Module**:
    ```bash
    sudo apt install libpam-google-authenticator -y
    google-authenticator
    ```
    - Scan the QR code or enter the provided secret key into the Google Authenticator app.
    - Save the emergency backup codes securely.
2. **Update PAM Configuration**: Edit `/etc/pam.d/sshd`:
    ```plaintext
    auth required pam_google_authenticator.so
    auth required pam_permit.so
    ```
3. **Update SSH Configuration**: Add the following to `/etc/ssh/sshd_config`:
    ```plaintext
    AuthenticationMethods publickey,keyboard-interactive
    PasswordAuthentication no
    ```
4. **Restart SSH**:
    ```bash
    sudo service ssh restart
    ```



### **5. Transfer Files to VPS**
- Use **SCP** to transfer resources securely:
```bash
scp -i <ssh-private-key> -r <source-directory> <username>@<IP/FQDN>:<destination-path>
```
- **Example**:
```bash
scp -i ~/.ssh/vps-ssh -r ~/Pentesting cry0l1t3@<vps-ip-address>:~/
```



### **Final Recommendations**
1. **Test Locally**:
    - Apply and verify hardening steps on a local VM before deploying to the VPS.
2. **Regular Monitoring**:
    - Review logs (e.g., `/var/log/auth.log`) for unusual activity.
    - Use monitoring tools to ensure server health and detect anomalies.
3. **Backup Critical Data**:
    - Regularly backup VPS configurations and resources.



### Questions
- What does the acronym Linux PAM stand for?
	- Pluggable Authentication Modules
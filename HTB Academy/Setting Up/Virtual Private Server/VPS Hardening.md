1. **System Updates**
	- Ensure your VPS is up-to-date to protect against vulnerabilities.
	- sudo apt update -y && sudo apt full-upgrade -y && sudo apt autoremove -y && sudo apt autoclean -y

2. **SSH Hardening**
	- **Edit SSH Configuration**:
	- Backup the original configuration file:
		- sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
	- Edit the SSH configuration:
		- sudo vim /etc/ssh/sshd_config
	- Make the following changes:
		- LogLevel VERBOSE
		- PermitRootLogin no
		- MaxAuthTries 3
		- MaxSessions 5
		- HostbasedAuthentication no
		- PermitEmptyPasswords no
		- ChallengeResponseAuthentication yes
		- UsePAM yes
		- X11Forwarding no
		- PrintMotd no
		- ClientAliveInterval 600
		- ClientAliveCountMax 0
		- AllowUsers "username"
		- Protocol 2
		- AuthenticationMethods publickey,keyboard-interactive
		- PasswordAuthentication no
		- **LogLevel VERBOSE**: For detailed logging.
		- **PermitRootLogin no**: Disallow root SSH access.
		- **MaxAuthTries 3**: Limit authentication attempts.
		- **MaxSessions 5**: Limit open sessions.
		- **HostbasedAuthentication no**: Disable host-based authentication.
		- **PermitEmptyPasswords no**: Disallow empty passwords.
		- **ChallengeResponseAuthentication yes**: Allow challenge-response authentication.
		- **UsePAM yes**: Use PAM for authentication.
		- **X11Forwarding no**: Disable X11 forwarding.
		- **PrintMotd no**: Disable message of the day.
		- **ClientAliveInterval 600**: Timeout interval.
		- **ClientAliveCountMax 0**: Number of allowed missed responses.
		- **AllowUsers "username"**: Limit SSH access to specific users.
		- **Protocol 2**: Use SSH protocol 2.
		- **AuthenticationMethods publickey,keyboard-interactive**: Require both public key and 2FA.
		- **PasswordAuthentication no**: Disable password authentication.

- **Restart SSH Service**:
	- sudo service ssh restart

#### **3. Install and Configure Fail2Ban**
- **Install Fail2Ban**:
	- sudo apt install fail2ban -y

- **Backup Configuration**:
	- sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.conf.bak

- **Configure Fail2Ban**:
	- Edit the Fail2Ban configuration:
		- sudo vim /etc/fail2ban/jail.conf

	- Update the `[sshd]` section:
		- [sshd]
		- enabled = true
		- bantime = 4w
		- maxretry = 3

#### **4. Configure Two-Factor Authentication (2FA)**
- **Install Google-Authenticator PAM Module**:
	- sudo apt install libpam-google-authenticator -y

- **Set Up Google Authenticator**:
	- google-authenticator
		- Follow the prompts to configure the OTP (One-Time Password) and scan the QR code with the Google Authenticator app.
		- Save emergency scratch codes securely.

- **Update PAM Configuration**:
	- Backup the PAM configuration:
		- sudo cp /etc/pam.d/sshd /etc/pam.d/sshd.bak

	- Edit the PAM configuration:
		- sudo vim /etc/pam.d/sshd

	- Add:
		- auth required pam_google_authenticator.so
		- auth required pam_permit.so

#### **5. Testing 2FA SSH Login**
- Test logging in with SSH:
	- ssh cry0l1t3@"vps-ip-address" -i ~/.ssh/vps-ssh
	- Enter the passphrase for the SSH key.
	- Provide the OTP from Google Authenticator.

#### **6. Transfer Resources**
- Use SCP to transfer files:
	- scp -i ~/.ssh/vps-ssh -r ~/Pentesting cry0l1t3@"vps-ip-address":~/

### **Closing Thoughts**
- **Practice**: Test these configurations in a local VM before applying them to a production VPS.
- **Configuration Replication**: Apply these hardening steps for both Windows and Linux systems as needed.
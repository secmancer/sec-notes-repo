- **Objective**: Harden the VPS to limit access to SSH and disable other services.
- **Principle**: Minimize attack vectors and secure SSH access rigorously. Avoid storing sensitive data on the VPS if possible.

#### Steps for Hardening
1. **System Update**
    - **Command**:
```
sudo apt update -y && sudo apt full-upgrade -y && sudo apt autoremove -y && sudo apt autoclean -y
```
**SSH Configuration**
- **File**: `/etc/ssh/sshd_config`
- **Backup**:
```
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
```
**Settings**:
- `LogLevel VERBOSE`
- `PermitRootLogin no`
- `MaxAuthTries 3`
- `MaxSessions 5`
- `HostbasedAuthentication no`
- `PermitEmptyPasswords no`
- `ChallengeResponseAuthentication yes`
- `UsePAM yes`
- `X11Forwarding no`
- `PrintMotd no`
- `ClientAliveInterval 600`
- `ClientAliveCountMax 0`
- `AllowUsers <username>`
- `Protocol 2`
- `AuthenticationMethods publickey,keyboard-interactive`
- `PasswordAuthentication no`

![[Screenshot_20240912_104853.png]]

**Fail2Ban Installation**
- **Command**:
```
sudo apt install fail2ban -y
```
- **Backup**:
```
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.conf.bak
```
**Configuration**:
- Edit `/etc/fail2ban/jail.conf`
- Un-comment and configure `[sshd]` section:
```
[sshd]
enabled = true
bantime = 4w
maxretry = 3
```

**2FA Authentication Setup**
- **Install Google-Authenticator PAM Module**:
```
sudo apt install libpam-google-authenticator -y
```
- **Generate Secret Key**:
```
google-authenticator
```
**PAM Configuration**:
- Backup file:
```
sudo cp /etc/pam.d/sshd /etc/pam.d/sshd.bak
```
- Edit `/etc/pam.d/sshd`:
```
#@include common-auth
auth required pam_google_authenticator.so
auth required pam_permit.so
```
**Update SSH Configuration**:
- Add to `/etc/ssh/sshd_config`:
```
AuthenticationMethods publickey,keyboard-interactive
PasswordAuthentication no
```
**Restart SSH**:
```
sudo service ssh restart
```

**Testing SSH Access**
- **Command**:
```
ssh <username>@<VPS-IP> -i <path-to-private-key>
```
- **Enter passphrase and verification code** from Google Authenticator.

**Transfer Resources**
- **SCP Syntax**:
```
scp -i <ssh-private-key> -r <directory-to-transfer> <username>@<IP/FQDN>:<path>
```
- **Example**:
```
scp -i ~/.ssh/vps-ssh -r ~/Pentesting <username>@<VPS-IP>:~/
```

### Questions
- What does the acronym Linux PAM stand for?
	- Pluggable Authentication Modules
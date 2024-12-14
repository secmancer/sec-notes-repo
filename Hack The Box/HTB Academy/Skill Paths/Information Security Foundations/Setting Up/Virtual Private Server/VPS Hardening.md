### Debrief
- Hardening the VPS system and access by limiting it to SSH and disabling all other services to minimize attack vectors.
- Avoid storing sensitive data on the VPS, especially for internal penetration tests.
- Secure the SSH server by implementing the following precautions:
    - Install Fail2ban.
    - Use SSH keys instead of passwords.
    - Reduce the idle timeout interval.
    - Disable password logins.
    - Disable X11 forwarding.
    - Use a non-standard SSH port.
    - Limit SSH user access.
    - Disable root logins.
    - Use SSH protocol 2.
    - Enable 2FA authentication for SSH.
- It’s recommended to test these settings in a local VM before applying them to the VPS.
- Ensure the VPS system is fully updated before applying hardening configurations.

### Update the Systems
```shell-session
[cry0l1t3@VPS ~]$ sudo apt update -y && sudo apt full-upgrade -y && sudo apt autoremove -y && sudo apt autoclean -y
```


### SSH Hardening
- SSH is always installed on the VPS, giving us guaranteed access to the server in advance. Now we can change some of the settings in the configuration file `/etc/ssh/sshd_config` to enforce these security measures for our SSH server. 
- In this file, we will comment out, change or add some lines. The entire list of possible settings that can be made for the SSH daemon can be found on the [man page](https://man.openbsd.org/sshd_config).
- #### Install Fail2Ban
```shell-session
[cry0l1t3@VPS ~]$ sudo apt install fail2ban -y
```
- Once we have installed it, we can find the configuration file at `/etc/fail2ban/jail.conf`. We should make a backup if we make a mistake somewhere and it does not work as it should.
- #### Fail2Ban Config Backup
```shell-session
[cry0l1t3@VPS ~]$ sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.conf.bak
```
- In this file, we will find the field commented out with `# [sshd]`. In most cases, we will find the first line commented out there. Otherwise, we add this and two more, as shown in the following example:
- #### /etc/fail2ban/jail.conf
```shell-session
...SNIP...

# [sshd]
enabled = true
bantime = 4w
maxretry = 3
```
- With this, we enable monitoring for the SSH server, set the `ban time` to four weeks, and allow a maximum of 3 `attempts`. 
- The advantage of this is that once we have configured our `2FA` feature for SSH, fail2ban will ban the IP address that has entered the `verification code` incorrectly three times too. 
- We should make the following configurations in the `/etc/ssh/sshd_config` file:
- #### Editing OpenSSH Config
```shell-session
[cry0l1t3@VPS ~]$ sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
[cry0l1t3@VPS ~]$ sudo vim /etc/ssh/sshd_config
```
![[Screenshot_20241107_152226.png]]
![[Screenshot_20241107_152235.png]]


### 2FA Authentication
- Enable 2-factor authentication (2FA) using Google Authenticator for increased security.
- Google Authenticator generates six-digit OTPs every 30 seconds, providing an additional authentication factor.
- The 2FA method offers high-security standards with relatively low implementation effort.
- Download and install Google Authenticator on Android or iOS from the respective app stores.
- Set up Google Authenticator on the VPS using the [Google-Authenticator PAM module](https://github.com/google/google-authenticator-libpam) for configuring 2FA.
- #### Installing Google-Authenticator PAM Module
```shell-session
[cry0l1t3@VPS ~]$ sudo apt install libpam-google-authenticator -y
[cry0l1t3@VPS ~]$ google-authenticator

Do you want authentication tokens to be time-based (y/n) y

Warning: pasting the following URL into your browser exposes the OTP secret to Google:
  https://www.google.com/chart?chs=200x200&chld=M|0&cht=qr&chl=otpauth://totp/cry0l1t3@parrot%3Fsecret%...SNIP...%26issuer%3Dparrot

   [ ---- QR Code ---- ]

Your new secret key is: ***************
Enter code from app (-1 to skip):
```
- A QR code and secret key will appear in the terminal, which we can scan with Google Authenticator or manually enter.
- After scanning or entering the secret key, Google Authenticator will display the first OTP (six-digit number) on the smartphone.
- Enter this OTP in the terminal to synchronize Google Authenticator on the smartphone and VPS.
- The module will generate emergency scratch codes (backup codes) as a backup, which should be stored securely.
- Backup codes can be used to log in if the smartphone is lost.
- #### Google-Authenticator Configuration
```shell-session
Enter code from app (-1 to skip): <Google-Auth Code>

Code confirmed
Your emergency scratch codes are:
  21323478
  43822347
  60232018
  73234726
  45456791
  
Do you want me to update your "/home/cry0l1t3/.google_authenticator" file? (y/n) y

Do you want to disallow multiple uses of the same authentication
token? This restricts you to one login about every 30s, but it increases
your chances to notice or even prevent man-in-the-middle attacks (y/n) y

By default, a new token is generated every 30 seconds by the mobile app.
In order to compensate for possible time-skew between the client and the server,
we allow an extra token before and after the current time. This allows for a
time skew of up to 30 seconds between authentication server and client. If you
experience problems with poor time synchronization, you can increase the window
from its default size of 3 permitted codes (one previous code, the current
code, the next code) to 17 permitted codes (the 8 previous codes, the current
code, and the 8 next codes). This will permit for a time skew of up to 4 minutes
between client and server.
Do you want to do so? (y/n) n

If the computer that you are logging into isn't hardened against brute-force
login attempts, you can enable rate-limiting for the authentication module.
By default, this limits attackers to no more than 3 login attempts every 30s.
Do you want to enable rate-limiting? (y/n) y
```
- Next, we need to configure the [PAM](https://en.wikipedia.org/wiki/Linux_PAM) module for the SSH daemon. To do this, we first create a backup of the file and open the file with a text editor such as Vim.
- #### 2FA PAM Configuration
```shell-session
[cry0l1t3@VPS ~]$ sudo cp /etc/pam.d/sshd /etc/pam.d/sshd.bak
[cry0l1t3@VPS ~]$ sudo vim /etc/pam.d/sshd
```
- We comment out the "`@include common-auth`" line by putting a "`#`" in front of it. Besides, we add two new lines at the end of the file, as follows:
- #### /etc/pam.d/sshd
```shell-session
#@include common-auth

...SNIP...

auth required pam_google_authenticator.so
auth required pam_permit.so
```
- Next, we need to adjust our settings in our SSH daemon to allow this authentication method. In this configuration file (`/etc/ssh/sshd_config`), we need to add two new lines at the end of the file as follows:
- #### /etc/ssh/sshd_config
```shell-session
...SNIP...

AuthenticationMethods publickey,keyboard-interactive
PasswordAuthentication no
```
- Finally, we have to restart the SSH server to apply the new configurations and settings.
- #### Restart SSH Server
```shell-session
[cry0l1t3@VPS ~]$ sudo service ssh restart
```
- Now we can test this and try to login to the SSH server with our SSH key and check if everything works as intended.
- #### 2FA SSH Login
```shell-session
secmancer@htb[/htb]$ ssh cry0l1t3@VPS -i ~/.ssh/vps-ssh

Enter passphrase for key 'cry0l1t3': *************
Verification code: <Google-Auth Code>
```
- Finally, we can transfer all our resources, scripts, notes, and other components to the VPS using [SCP](https://en.wikipedia.org/wiki/Secure_copy_protocol).
- #### SCP Syntax
```shell-session
secmancer@htb[/htb]$ scp -i <ssh-private-key> -r <directory to transfer> <username>@<IP/FQDN>:<path>
```
- #### Resources Transfer
```shell-session
secmancer@htb[/htb]$ scp -i ~/.ssh/vps-ssh -r ~/Pentesting cry0l1t3@VPS:~/

Enter passphrase for key 'cry0l1t3': *************
Verification code: <Google-Auth Code>
```


### Questions
- What does the acronym Linux PAM stand for?
	- Pluggable Authentication Modules
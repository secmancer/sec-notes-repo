### Interactive
- An interactive, or local logon session, is initiated by a user authenticating to a local or domain system by entering their credentials.
- An interactive logon can be initiated by logging directly into the system, by requesting a secondary logon session using the `runas` command via the command line, or through a Remote Desktop connection.



### Non-interactive
- Non-interactive accounts in Windows differ from standard user accounts as they do not require login credentials. 
- There are 3 types of non-interactive accounts: the Local System Account, Local Service Account, and the Network Service Account. 
- Non-interactive accounts are generally used by the Windows operating system to automatically start services and applications without requiring user interaction. 
- These accounts have no password associated with them and are usually used to start services when the system boots or to run scheduled tasks.
- There are differences between the three types of accounts, which is shown in the table below.
![[Screenshot_20241109_111942.png]]

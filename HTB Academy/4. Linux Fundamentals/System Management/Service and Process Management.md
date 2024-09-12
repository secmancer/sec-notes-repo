**Types of Services:**
- **Internal Services:** Required at system startup for hardware-related tasks.
- **User-Installed Services:** Include server services running in the background, known as daemons. These services often have a `d` at the end of their names (e.g., `sshd`, `systemd`).

**systemd:**
- Most Linux distributions use `systemd` as the Init system.
- `systemd` has a process ID (PID) of 1 and manages the starting and stopping of other services.
- All processes have a PID, viewable under `/proc/`. Processes can have a parent process ID (PPID), and those with a PPID are child processes.

![[Screenshot_20240912_135605.png]]

**Managing Services with `systemctl`:**
- **Start a Service:**
```
systemctl start <service>
```
- Example:
```
systemctl start ssh
```
- **Check Service Status**:
```
systemctl status <service>
```
- Example:
```
systemctl status ssh
```
- **Enable a Service to Start at Boot**:
```
systemctl enable <service>
```
- Example:
```
systemctl enable ssh
```
- **List All Services:**
```
systemctl list-units --type=service
```
- **View Logs for a Service:**
```
journalctl -u <service> --no-pager
```
- Example:
```
journalctl -u ssh.service --no-pager
```

**Managing Processes:**
- **View All Signals:**
```
kill -l
```
**Common Signals:**
- `1` - SIGHUP: Terminal closed.
- `2` - SIGINT: User interrupts with [Ctrl] + C.
- `9` - SIGKILL: Forcefully kill a process.
- `15` - SIGTERM: Terminate gracefully.
- `19` - SIGSTOP: Stop the process, cannot be handled.
- `20` - SIGTSTP: Suspend process with [Ctrl] + Z.


**Kill a Process:**
```
kill -9 <PID>
```
Example:
```
kill -9 1234
```

**Background and Foreground Processes:**
- **Suspend a Process:** Use [Ctrl + Z] to suspend a running process.
- **List Background Processes:**
```
jobs
```
- **Resume a Process in Background:**
```
bg
```
- **Run a Process in Background Directly:**
```
<command> &
```
- Example:
```
ping -c 10 www.hackthebox.eu &
```
- **Bring a Background Process to Foreground:**
```
fg <ID>
```
- Example:
```
fg 1
```


**Executing Multiple Commands:**
- **Semicolon `;`:** Executes commands sequentially, regardless of success or failure.
```
echo '1'; echo '2'; echo '3'
```
- **Double Ampersand `&&`:** Executes the next command only if the previous command succeeds.
```
echo '1' && ls MISSING_FILE && echo '3'
```
- **Pipes `|`:** Passes the output of one command as input to another.
```
command1 | command2
```

### Questions
- Use the "systemctl" command to list all units of services and submit the unit name with the description "Load AppArmor profiles managed internally by snapd" as the answer.
	- snapd.apparmor.service
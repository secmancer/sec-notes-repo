### Types of Services

- **Internal Services**: Required at system startup for hardware-related tasks.
- **User-Installed Services**: Run in the background without user interaction, also known as daemons (e.g., `sshd`, `systemd`).

### Systemd

- **systemd**: The Init process with PID 1, responsible for managing other services.
- **Processes**: Assigned a PID viewable under `/proc/`. Processes with a parent process ID (PPID) are known as child processes.

![[Screenshot_20240812_140725 1.png]]

![[Screenshot_20240812_142443.png]]

![[Screenshot_20240812_142454.png]]


![[Screenshot_20240812_142508.png]]

![[Screenshot_20240812_142517.png]]

![[Screenshot_20240812_142524.png]]

![[Screenshot_20240812_142534.png]]

![[Screenshot_20240812_142541.png]]
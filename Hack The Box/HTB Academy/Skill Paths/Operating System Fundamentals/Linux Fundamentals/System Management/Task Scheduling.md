### **Overview**
- Task scheduling automates the execution of tasks at specific times or intervals.
- Common use cases:
    - Automatic software updates
    - Script execution
    - Database maintenance
    - Backup automation
    - Alerts and notifications for events
- Important for cybersecurity professionals to detect unauthorized scheduled tasks (e.g., cron jobs used for persistence).



### **1. Systemd Task Scheduling**
- #### **Steps to Create a Systemd Timer**
	1. **Create a Timer**
    ```sh
    sudo mkdir /etc/systemd/system/mytimer.timer.d
    sudo vim /etc/systemd/system/mytimer.timer
    ```
	- **Example Timer Configuration (`mytimer.timer`)**
    ```ini
    [Unit]
    Description=My Timer
    
    [Timer]
    OnBootSec=3min
    OnUnitActiveSec=1hour
    
    [Install]
    WantedBy=timers.target
    ```
    
    - `OnBootSec=3min` → Runs once after boot
    - `OnUnitActiveSec=1hour` → Runs at regular intervals
```
	2. **Create a Service**
    ```sh
    sudo vim /etc/systemd/system/mytimer.service
    ```
	- **Example Service Configuration (`mytimer.service`)**
    ```ini
    [Unit]
    Description=My Service
    
    [Service]
    ExecStart=/full/path/to/my/script.sh
    
    [Install]
    WantedBy=multi-user.target
    ```
    
    - Defines the script to execute (`ExecStart`)
```
	3. **Reload and Start Systemd Timer**    
    ```sh
    sudo systemctl daemon-reload
    sudo systemctl start mytimer.timer
    sudo systemctl enable mytimer.timer
    ```
    - Ensures `mytimer.service` runs according to `mytimer.timer`



### **2. Cron Task Scheduling**
- Uses `crontab` to store scheduled tasks.
- Structure:
    ```
    ┌──────── Minute (0-59)
    │ ┌────── Hour (0-23)
    │ │ ┌──── Day of Month (1-31)
    │ │ │ ┌── Month (1-12)
    │ │ │ │ ┌─ Day of Week (0-7, Sun=0/7)
    │ │ │ │ │
    * * * * * command-to-execute
    ```
- #### **Example `crontab` Entries**
```sh
# System Update every 6 hours
0 */6 * * * /path/to/update_software.sh

# Execute scripts on the 1st of each month at midnight
0 0 1 * * /path/to/scripts/run_scripts.sh

# Cleanup DB every Sunday at midnight
0 0 * * 0 /path/to/scripts/clean_database.sh

# Backups every Sunday at midnight
0 0 * * 7 /path/to/scripts/backup.sh
```
- Logs and notifications can be set up for monitoring execution.



### **3. Systemd vs. Cron**

|Feature|Systemd Timers|Cron Jobs|
|---|---|---|
|**Configuration**|Uses `*.timer` and `*.service` files|Uses `crontab`|
|**Flexibility**|Can trigger tasks based on system events|Runs at fixed intervals|
|**Logging**|Integrated logging via `journalctl`|Needs additional logging setup|
|**Reliability**|More robust and error-resistant|Simpler but lacks built-in error handling|
- Systemd is preferred for system-level tasks, while Cron is easier for user-level task automation.



### **Key Takeaways**
- **Systemd** is event-driven and better for system-level automation.
- **Cron** is simpler but less flexible, suited for user tasks.
- Both tools can be leveraged for penetration testing to identify persistence mechanisms.



### Questions
- What is the Type of the service of the "dconf.service"?
	- dbus
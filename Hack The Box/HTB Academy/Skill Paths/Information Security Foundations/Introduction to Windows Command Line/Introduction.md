## Introduction
- Windows includes **CMD.exe (Command Prompt)** and **PowerShell**, two powerful command-line interfaces for system administration, automation, and penetration testing.



## **Command Prompt vs. PowerShell**

| Feature                        | PowerShell                                    | Command Prompt                     |
| ------------------------------ | --------------------------------------------- | ---------------------------------- |
| **Year Introduced**            | 2006                                          | 1981                               |
| **Command Compatibility**      | Can run batch commands & PowerShell cmdlets   | Can only run batch commands        |
| **Command Aliases**            | Yes                                           | No                                 |
| **Piping Output**              | Supports passing output between cmdlets       | No direct piping support           |
| **Output Type**                | Objects                                       | Text                               |
| **Command Execution**          | Can execute multiple cmdlets in scripts       | Must execute one command at a time |
| **Scripting Support**          | Has an Integrated Scripting Environment (ISE) | No ISE                             |
| **Programming Library Access** | Built on .NET framework                       | Cannot access .NET libraries       |
| **Cross-Platform Support**     | Can run on Linux                              | Windows only                       |

- PowerShell is a **more powerful scripting tool** with object-oriented output and automation capabilities, while Command Prompt is more **limited and static**.



## **Connecting to Windows Hosts via SSH**
- To connect to a remote Windows machine using SSH, use the following format:
```sh
ssh htb-student@<IP-Address>
```
- **First-time login**: Accept the host's certificate.  
- **Provide password** when prompted.  
- Once authenticated, you can start executing **PowerShell** or **CMD commands**.



## **Next Steps**  
- Learn **basic PowerShell commands** and scripting.  
- Practice **command execution & automation**.  
- Explore **PowerShell cmdlets** and their real-world applications.  
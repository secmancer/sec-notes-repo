### PowerShell Object-Based Search and Filtering
**Overview:** Effective searching, finding, and filtering content is crucial for using the Command-Line Interface (CLI) effectively, regardless of the shell or operating system. In PowerShell, this process is enhanced by its object-oriented nature. This section will explain how PowerShell uses objects, filtering based on properties and content, and the PowerShell Pipeline.

**PowerShell Output and Objects:**
- **Objects in PowerShell:**
    - Unlike Bash or cmd, where output is typically plain text, PowerShell outputs objects.
    - **Object:** An individual instance of a class. For example, a computer is an object made up of various components.
- **Class:**
    - A class is a blueprint or schema that defines the properties and methods of an object. It describes how an object should be assembled and what it comprises.
- **Properties:**
    - Properties are the data associated with an object. For a computer, these would be components like the CPU, RAM, and hard drive. Each property has a specific role and value within the object.
- **Methods:**
    - Methods are functions or actions that an object can perform. For a computer, methods could include processing data, accessing the internet, or running software applications.


**Understanding Object Interactions:**
- By grasping how PowerShell handles objects, classes, properties, and methods, you can effectively interact with and manipulate these objects.
- **Defining Object Types:**
    - With a clear understanding of these concepts, you can define your own object types and interact with them according to their properties and methods.


**Filtering and Finding Objects in PowerShell:**
- **Filtering Based on Properties:**
    - PowerShell allows you to filter objects based on their properties. You can use cmdlets like `Where-Object` to specify conditions that must be met for an object to be included in the results.
- **Using the PowerShell Pipeline:**
    - The Pipeline is a powerful feature in PowerShell that lets you pass the output of one cmdlet as input to another. This allows for chaining commands and performing complex filtering and processing.


### Finding and Filtering Objects in PowerShell
**Overview:** In PowerShell, searching for and filtering objects is crucial for managing and retrieving specific data efficiently. This involves understanding the structure of objects, their properties, and methods. Let’s explore how to work with these concepts through practical examples.

**Understanding Objects:**
- **Example Object: User**
    - **User Object:** Represents a user account with various properties and methods.
    - **Properties and Methods:** Each user object has specific properties and methods that define its attributes and actions.

**Getting Object Properties and Methods:**
- **Command:**
```
Get-LocalUser administrator | Get-Member
```
- **Output Example:**
```
Name                   MemberType Definition
----                   ---------- ----------
Clone                  Method     Microsoft.PowerShell.Commands.LocalUser Clone()
Equals                 Method     bool Equals(System.Object obj)
GetHashCode            Method     int GetHashCode()
GetType                Method     type GetType()
ToString               Method     string ToString()
AccountExpires         Property   System.Nullable[datetime] AccountExpires {get;set;}
Description            Property   string Description {get;set;}
Enabled                Property   bool Enabled {get;set;}
FullName               Property   string FullName {get;set;}
LastLogon              Property   System.Nullable[datetime] LastLogon {get;set;}
Name                   Property   string Name {get;set;}
ObjectClass            Property   string ObjectClass {get;set;}
PasswordChangeableDate Property   System.Nullable[datetime] PasswordChangeableDate {get;set;}
PasswordExpires        Property   System.Nullable[datetime] PasswordExpires {get;set;}
PasswordLastSet        Property   System.Nullable[datetime] PasswordLastSet {get;set;}
PasswordRequired       Property   bool PasswordRequired {get;set;}
PrincipalSource        Property   System.Nullable[Microsoft.PowerShell.Commands.PrincipalSource] PrincipalSource {get;set;}
SID                    Property   System.Security.Principal.SecurityIdentifier SID {get;set;}
UserMayChangePassword  Property   bool UserMayChangePassword {get;set;}
```


**Viewing Object Properties:**
- **Command:**
```
Get-LocalUser administrator | Select-Object -Property *
```
- **Output Example:**
```
AccountExpires         :
Description            : Built-in account for administering the computer/domain
Enabled                : False
FullName               :
PasswordChangeableDate :
PasswordExpires        :
UserMayChangePassword  : True
PasswordRequired       : True
PasswordLastSet        :
LastLogon              : 1/20/2021 5:39:14 PM
Name                   : Administrator
SID                    : S-1-5-21-3916821513-3027319641-390562114-500
PrincipalSource        : Local
ObjectClass            : User
```


**Filtering Object Properties:**
- **Command:**
```
Get-LocalUser * | Select-Object -Property Name, PasswordLastSet
```
- **Output Example:**
```
Name               PasswordLastSet
----               ---------------
Administrator
DefaultAccount
Guest
MTanaka              1/27/2021 2:39:55 PM
WDAGUtilityAccount 1/18/2021 7:40:22 AM
```



**Sorting and Grouping Objects:**
- **Sorting:**
```
Get-LocalUser * | Sort-Object -Property Name
```
- **Grouping:**
```
Get-LocalUser * | Sort-Object -Property Name | Group-Object -Property Enabled
```
- **Output Example:**
```
Count Name                      Group
----- ----                      -----
    4 False                     {Administrator, DefaultAccount, Guest, WDAGUtilityAccount}
    1 True                      {MTanaka}
```
- **Benefit:** Quickly identify relevant services (e.g., security tools) to plan further actions.

**Why Filtering is Important:**
1. **Manage Large Data Sets:**
    - Filtering helps in handling large volumes of data by narrowing down to relevant information.
2. **Increase Efficiency:**
    - By focusing on specific properties or criteria, filtering reduces the time needed to analyze data.
3. **Contextual Relevance:**
    - Filtering ensures that only pertinent information is reviewed, aiding in decision-making and action planning.


**Practical Use Cases:**
- **Penetration Testing:** Identifying defensive measures running on a host.
- **System Administration:** Monitoring specific services or system statuses.
- **Troubleshooting:** Isolating issues by focusing on relevant services or properties.


PowerShell provides various ways to evaluate and filter data based on object values and properties. This is crucial for narrowing down results to only the relevant information. Evaluation expressions and comparison operators play a key role in this process.

![[Screenshot_20240915_215159.png]]

**Filtering with Comparison Operators:**
- **Comparison Operators Recap:**
    - **`-eq`**: Equals
    - **`-ne`**: Not Equals
    - **`-gt`**: Greater Than
    - **`-lt`**: Less Than
    - **`-ge`**: Greater Than or Equal To
    - **`-le`**: Less Than or Equal To
    - **`-like`**: Matches a pattern with wildcards (`*`)
    - **`-notlike`**: Does not match a pattern with wildcards (`*`)
    - **`-match`**: Matches a regular expression
    - **`-notmatch`**: Does not match a regular expression

**Filtering Example:**
```
Get-Service | Where-Object { $_.DisplayName -like '*Defender*' }
```
- Filters services with "Defender" in their `DisplayName`.


**Filtering Specifics:**
- **Defender Services:**
```
Get-Service | Where-Object { $_.DisplayName -like '*Defender*' } | Select-Object -Property *
```
- Displays all properties of services associated with Windows Defender.



**PowerShell Pipeline (|):**
- **Overview:**
    - **Pipeline** allows chaining commands together, passing the output of one command as input to the next.
    - Commands are executed from left to right.
    - Example:
```
Command-1 | Command-2 | Command-3
```
- **Pipeline Variations:**
```
Command-1 |
  Command-2 |
    Command-3
```

```
Get-Process | Where-Object CPU | Where-Object Path | Get-Item
```

**Example of Using Pipeline:**
```
Get-Process | Sort-Object | Get-Unique | Measure-Object
```
- **`Get-Process`**: Retrieves the list of processes.
- **`Sort-Object`**: Sorts the processes.
- **`Get-Unique`**: Filters unique processes.
- **`Measure-Object`**: Counts the unique processes.


**Practical Application of Pipeline:**
- **Counting Unique Processes:**
```
Get-Process | Sort-Object | Get-Unique | Measure-Object
```
- Outputs the total count of unique processes.


**Complex Uses:**
- Sorting log entries
- Filtering specific event codes
- Processing large data sets (e.g., databases)



**Overview of Pipeline Chain Operators:**
- **Operators:**
    - **`&&`**: Executes the next command if the preceding command succeeds.
    - **`||`**: Executes the next command if the preceding command fails.
- **Support:**
    - Windows PowerShell 5.1 and older versions do not support these operators.
    - To use these features, install PowerShell 7 alongside Windows PowerShell.



**Using `&&` and `||`:**
- **Example 1: Conditional Execution with `&&`**
```
Get-Content '.\test.txt' && ping 8.8.8.8
```
- If `Get-Content` successfully reads the file, `ping` command will execute.
- **Output:**
    - Displays content of `test.txt`.
    - Executes the `ping` command, showing the results of the ping test.
- **Example 2: Conditional Execution with `||`**
```
Get-Content '.\test.txt' || ping 8.8.8.8
```
- If `Get-Content` fails to read the file, `ping` command will execute.
- **Output:**
    - Displays the results of `ping` command if `Get-Content` fails.
- Example 3: Handling File Not Found with `||`
```
Get-Content '.\testss.txt' || ping 8.8.8.8
```
- If `Get-Content` fails because the file does not exist, `ping` command will execute.
- **Output:**
    - Displays the `ping` results since the file was not found.


**Benefits of Pipeline Chain Operators:**
- **Efficiency:** Allows conditional execution of commands in a single line, saving time and effort.
- **Error Handling:** Helps handle errors gracefully by specifying what to do if a command fails.
- **Streamlined Execution:** Combines multiple commands into one line, making scripts more concise and easier to manage.



**Application in Penetration Testing:**
- **Searching and Enumeration:**
    - Useful for tasks like searching for strings or data within files and directories.
    - Helps in maintaining stealth and avoiding the introduction of new tools into the environment.



When tools like Snaffler or Winpeas aren't available, you can still hunt for sensitive information (credentials, keys, etc.) using PowerShell cmdlets. Combining `Get-ChildItem`, `Select-String`, and `Where-Object` helps in searching through file systems for relevant data.


**Key Cmdlets:**
- **`Select-String` (alias `sls`):**
    - Similar to `grep` in Linux or `findstr` in Windows Command-Prompt.
    - Performs regular expression (regex) pattern matching on input strings and file contents.
    - Outputs matching lines, file names, and line numbers by default.
    - Use `-CaseSensitive` for case-sensitive searches.
- **`Get-ChildItem`:**
    - Retrieves items from a specified path.
    - Useful for listing files and directories.
- **`Where-Object`:**
    - Filters output based on specified conditions.



**Finding Interesting Files:**
```
Basic Search:
Get-ChildItem -Path C:\Users\MTanaka\ -File -Recurse
Lists all files in the specified directory and its subdirectories.


Narrowing Search by File Type:
Get-ChildItem -Path C:\Users\MTanaka\ -File -Recurse -ErrorAction SilentlyContinue | Where-Object { $_.Name -like "*.txt" }
Filters files with the `.txt` extension.


Expanding Search to Multiple File Types:
Get-ChildItem -Path C:\Users\MTanaka\ -File -Recurse -ErrorAction SilentlyContinue | Where-Object { $_.Name -like "*.txt" -or $_.Name -like "*.py" -or $_.Name -like "*.ps1" -or $_.Name -like "*.md" -or $_.Name -like "*.csv" }
Filters files with extensions `.txt`, `.py`, `.ps1`, `.md`, and `.csv`.
```

**Searching File Contents:**
- **Basic Search Query:**
```
Get-ChildItem -Path C:\Users\MTanaka\ -Filter "*.txt" -Recurse -File | Select-String "Password","credential","key"
```
- Searches contents of `.txt` files for keywords like "Password", "credential", and "key".
- **Combining File Search with Content Search:**
```
Get-ChildItem -Path C:\Users\MTanaka\ -File -Recurse -ErrorAction SilentlyContinue | Where-Object { $_.Name -like "*.txt" -or $_.Name -like "*.py" -or $_.Name -like "*.ps1" -or $_.Name -like "*.md" -or $_.Name -like "*.csv" } | Select-String "Password","credential","key","UserName"
```
- Filters files and searches their contents for additional keywords like "UserName".


**Practical Considerations:**
- **Error Handling:**
    - Use `-ErrorAction SilentlyContinue` to ensure the pipeline continues even if some files or directories are unreadable.
- **Optimization:**
    - Combine file search and content search efficiently to streamline data retrieval.
    - Adjust search keywords based on the specific context or information you're targeting.


When searching for valuable files and data on a host, consider checking the following directories and locations:
1. **Users `\AppData\` Folder:**
    - **Location:** `C:\Users\<USERNAME>\AppData\`
    - **Purpose:** Many applications store configuration files, temporary saves, and more in this folder.
    - **Command:**
```
Get-ChildItem -Path C:\Users\<USERNAME>\AppData\ -Recurse
```
2. **Users Home Folder:**
	- **Location:** `C:\Users\<USERNAME>\`
	- **Purpose:** Common storage place for VPN keys, SSH keys, and other important files. Hidden folders often contain sensitive data.
	- **Command to include hidden files:**
```
Get-ChildItem -Path C:\Users\<USERNAME>\ -Recurse -Hidden
```
3. **Console History Files:**
	- **Location 1:** `C:\Users\<USERNAME>\AppData\Roaming\Microsoft\Windows\Powershell\PSReadline\ConsoleHost_history.txt`
	- **Location 2:** `(Get-PSReadlineOption).HistorySavePath`
	- **Purpose:** Contains command history which can be insightful, especially on administrator hosts.
	- **Commands:**
```
Get-Content "C:\Users\<USERNAME>\AppData\Roaming\Microsoft\Windows\Powershell\PSReadline\ConsoleHost_history.txt"
Get-Content (Get-PSReadlineOption).HistorySavePath
```
4. **Clipboard Content:**
- **Command:**
```
Get-Clipboard
```
- **Purpose:** Might contain recently copied sensitive information.
5. **Scheduled Tasks:**
	- **Purpose:** Can reveal scripts or programs scheduled to run at specific times, which might include sensitive information or clues.
	- **Command:**
```
Get-ScheduledTask
```



**Tips:**
- **Customization:** Tailor your search based on the context and what you’re specifically looking for.
- **Error Handling:** Ensure commands handle errors gracefully to avoid missing potential data.



## Questions
- What defines the functions our objects have?
	- Methods
- What Cmdlet can show us the properties and methods of an object?
	- Get-Member
- If we wanted to look through a directory and all sub-directories for something, what modifier would we use with the Get-ChildItem Cmdlet?
	- -Recurse
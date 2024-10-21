### Nmap Output Formats

Nmap provides different options to **save scan results** in various formats, each useful for different purposes like further analysis or reporting.

- **Normal output** (`-oN`): Saved with the `.nmap` extension.
- **Grepable output** (`-oG`): Saved with the `.gnmap` extension.
- **XML output** (`-oX`): Saved with the `.xml` extension.

For convenience, you can save results in **all formats simultaneously** using the `-oA` option. This creates three output files with the same base name but different extensions.

#### Example Command:
```bash
sudo nmap 10.129.2.28 -p- -oA target
```
- **`10.129.2.28`**: The target IP address.
- **`-p-`**: Scans all ports.
- **`-oA target`**: Saves the results as `target.nmap`, `target.gnmap`, and `target.xml`.

---

### Nmap Scan Example
```
Nmap scan report for 10.129.2.28
Host is up (0.0091s latency).
PORT      STATE SERVICE
22/tcp    open  ssh
25/tcp    open  smtp
80/tcp    open  http
MAC Address: DE:AD:00:00:BE:EF (Intel Corporate)
```
- **Scan Duration**: 10.22 seconds
- **Results**: 
  - **Ports open**: 22 (SSH), 25 (SMTP), 80 (HTTP)
  - **Host up**: Detected with 0.0091s latency.

---

### File Formats

1. **Normal Output (`.nmap` file)**:
    - Plain-text format showing a human-readable scan summary.
    - Includes port status, service identification, and host information.
    ```bash
    Nmap scan report for 10.129.2.28
    Host is up (0.053s latency).
    PORT   STATE SERVICE
    22/tcp open  ssh
    25/tcp open  smtp
    80/tcp open  http
    MAC Address: DE:AD:00:00:BE:EF (Intel Corporate)
    ```

2. **Grepable Output (`.gnmap` file)**:
    - Designed for easy parsing with command-line tools like `grep`.
    - Useful for automated analysis.
    ```bash
    Host: 10.129.2.28 ()	Status: Up
    Ports: 22/open/tcp//ssh///, 25/open/tcp//smtp///, 80/open/tcp//http///
    ```

3. **XML Output (`.xml` file)**:
    - Structured format, suitable for importing into other tools or generating reports.
    - Can be converted to HTML using `xsltproc`.
    ```xml
    <nmaprun>
      <host>
        <address addr="10.129.2.28" addrtype="ipv4"/>
        <port protocol="tcp" portid="22">
          <state state="open"/>
          <service name="ssh"/>
        </port>
        <port protocol="tcp" portid="25">
          <state state="open"/>
          <service name="smtp"/>
        </port>
        <port protocol="tcp" portid="80">
          <state state="open"/>
          <service name="http"/>
        </port>
      </host>
    </nmaprun>
    ```

---

### Converting XML to HTML
- **Purpose**: Converts the XML output into a more readable HTML format, useful for documentation.
- **Command**: 
    ```bash
    xsltproc target.xml -o target.html
    ```
    - Converts `target.xml` to `target.html`.
    - When opened in a browser, it provides a clear and structured view of the scan results.

---

### Summary of Key Options:
- **`-oN`**: Saves output as plain text.
- **`-oG`**: Saves output in grepable format.
- **`-oX`**: Saves output in XML.
- **`-oA`**: Saves results in all formats (plain text, grepable, XML).

These output formats allow flexibility in how results are stored, analyzed, or presented, especially useful for both technical and non-technical audiences.

More information about the output formats can be found at: [https://nmap.org/book/output.html](https://nmap.org/book/output.html)

## Questions
- Perform a full TCP port scan on your target and create an HTML report. Submit the number of the highest port as the answer.
	- 31337
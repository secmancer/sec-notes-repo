### Application Management Notes: macOS
- #### Introduction
	- **Extending macOS functionality** involves installing new software and tools.
	- **Risks**: Unintentional installation of malware or adware.
	- **Focus**: Methods of installing applications, setting up macOS for pentesting, and using package managers like **Homebrew**.



### App Store
- **Primary source** for downloading applications.
- **Steps**:
  1. Open the **App Store** app.
  2. Search for the desired app.
  3. Click **GET** (free) or the price (paid) to download.
  4. Launch the app from the **Applications** directory.
- **Uninstallation**:
  - Drag the app from the **Applications** folder to the **Trash**.



### Third-Party Applications
- **Downloading**:
  - Vendors host applications on their websites.
  - Example: Downloading **Google Chrome**:
    1. Search for "Google Chrome Download."
    2. Download the application bundle.
- **Installation Methods**:
  1. **Drag-and-Drop**:
     - Drag the application bundle to the **Applications** folder.
     - Example: Google Chrome.
  2. **Installer**:
     - Run the installer for applications like **Adobe CC** or **Microsoft Office**.
     - Follow the installation wizard.
     - Use the bundled **uninstaller** for removal.



### Homebrew
- **Overview**:
  - Free, open-source **package manager** for macOS.
  - Simplifies installation of developer and pentesting tools.
  - Avoids manual compilation of open-source tools.
- **Installation**:
  - Run the following command:
    ```bash
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    ```
  - Verify installation:
    ```bash
    brew -v
    ```
- **Installing Tools**:
  - Example: Install **PHP**:
    ```bash
    brew install php
    ```
  - Uninstall:
    ```bash
    brew uninstall php
    ```
  - Search for packages:
    ```bash
    brew search firefox
    ```
- **Homebrew Cask**:
  - Installs **GUI applications**.
  - Example: Install **Firefox**:
    ```bash
    brew install firefox --cask
    ```



### macOS for Pentesting
- **Popularity**:
  - macOS is widely used by developers and security experts.
  - Many pentesting tools have macOS versions.
- **Virtual Machines (VMs)**:
  - **Recommended** for pentesting exercises.
  - **Benefits**:
    - Sandboxed environment.
    - Avoids harm to the main OS.
  - **Virtualization Software**:
    - **VMWare**, **Parallels**, **VirtualBox**.
  - **Steps**:
    1. Install virtualization software.
    2. Download the ISO for the desired OS.
    3. Follow the installation instructions.
- **Direct Installation on macOS**:
  - **Safe Tools**:
    - **Nmap**, **Burp Suite**, **PowerShell**, **Ghidra**, **VSCode**.
  - **Install via Homebrew**:
    ```bash
    brew install nmap burp-suite powershell ghidra visual-studio-code
    ```



### Common Pentesting Tools on macOS
- **Pre-installed Scripting Languages**:
  - **Bash**, **Python**.
- **Tools with macOS Versions**:
  - **Nmap**
  - **Burp Suite**
  - **PowerShell**
  - **Ghidra**
  - **VSCode**
- **Install via Homebrew**:
  - **Nmap**
  - **Burp Suite**
  - **PowerShell**
  - **Ghidra**
  - **VSCode**
  - **SQLMap**
  - **VirtualBox**



### Summary
- **App Store**: Primary source for trusted applications.
- **Third-Party Applications**: Download from vendor websites; use drag-and-drop or installers.
- **Homebrew**: Essential for developers and pentesters; simplifies tool installation.
- **Pentesting on macOS**:
  - Use **VMs** for sandboxed environments.
  - Directly install safe tools like **Nmap**, **Burp Suite**, and **Ghidra**.
  - Leverage **Homebrew** for easy installation of pentesting tools.



### Questions
- Search 'homebrew' for 'tmux', and one of the results ends in 'nator'. What is the full name of this package?
	- tmuxinator
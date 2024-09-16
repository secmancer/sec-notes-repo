Package management is crucial for maintaining Linux systems, whether for system administration, personal use, or building/upgrading penetration testing distributions.

#### Key Features of Package Management Systems
- **Package Downloading**: Retrieve software packages from repositories.
- **Dependency Resolution**: Automatically handle dependencies required by packages.
- **Standard Binary Package Format**: Use common formats like `.deb` (Debian-based) and `.rpm` (Red Hat-based).
- **Common Installation and Configuration Locations**: Ensure consistent file locations for installed software.
- **Additional System-Related Configuration and Functionality**: Manage system-wide settings and functionalities.
- **Quality Control**: Ensure software packages are reliable and up-to-date.

#### Common Package Managers and Commands
- **`dpkg`**:
    - **Description**: Tool to install, build, remove, and manage Debian packages. `aptitude` is a more user-friendly front-end.
    - **Usage**: `dpkg [options] [package_file.deb]`
- **`apt`**:
    - **Description**: High-level command-line interface for package management on Debian-based systems.
    - **Usage**: `apt [options] [command]`
    - **Examples**: `apt update`, `apt upgrade`, `apt install [package_name]`
- **`aptitude`**:
    - **Description**: Alternative to `apt`, provides a high-level interface to the package manager.
    - **Usage**: `aptitude [options] [command]`
- **`snap`**:
    - **Description**: Manage snap packages for secure distribution of apps across various platforms.
    - **Usage**: `snap [options] [command]`
    - **Examples**: `snap install [package_name]`, `snap remove [package_name]`
- **`gem`**:
    - **Description**: Front-end for RubyGems, the standard package manager for Ruby.
    - **Usage**: `gem [options] [command]`
    - **Examples**: `gem install [gem_name]`, `gem update [gem_name]`
- **`pip`**:
    - **Description**: Python package installer for packages not available in the Debian archive. Works with version control repositories.
    - **Usage**: `pip [options] [command]`
    - **Examples**: `pip install [package_name]`, `pip list`
- **`git`**:
    - **Description**: Distributed version control system with rich command set for managing code repositories.
    - **Usage**: `git [options] [command]`
    - **Examples**: `git clone [repository_url]`, `git pull`

![[Screenshot_20240912_135152.png]]

#### Working with APT (Advanced Package Tool)
- **View Repository List**:
    - **Command**: `cat /etc/apt/sources.list.d/[file_name]`
    - **Example**:
```
secmancer@htb[/htb]$ cat /etc/apt/sources.list.d/parrot.list
# parrot repository
deb http://htb.deb.parrot.sh/parrot/ rolling main contrib non-free
```


**Search for Packages**:
- **Command**: `apt-cache search [search_term]`
- **Example**:
```
secmancer@htb[/htb]$ apt-cache search impacket
```

**Show Package Details**:
- **Command**: `apt-cache show [package_name]`
- **Example**:
```
secmancer@htb[/htb]$ apt-cache show impacket-scripts
```

**List Installed Packages**:
- **Command**: `apt list --installed`
- **Example**:
```
secmancer@htb[/htb]$ apt list --installed
```

**Install a Package**:
- **Command**: `sudo apt install [package_name] -y`
- **Example**:
```
secmancer@htb[/htb]$ sudo apt install impacket-scripts -y
```


#### Working with DPKG
- **Install a Package from .deb File**:
    - **Command**: `sudo dpkg -i [package_file.deb]`
    - **Example**:
```
secmancer@htb[/htb]$ sudo dpkg -i strace_4.21-1ubuntu1_amd64.deb
```

#### Example Workflow
1. **Install Git**:
```
secmancer@htb[/htb]$ sudo apt install git
```
2. **Clone a Repository**:
```
secmancer@htb[/htb]$ mkdir ~/nishang/ && git clone https://github.com/samratashok/nishang.git ~/nishang
```
3. **Download and Install a .deb Package**:
```
secmancer@htb[/htb]$ wget http://archive.ubuntu.com/ubuntu/pool/main/s/strace/strace_4.21-1ubuntu1_amd64.deb
secmancer@htb[/htb]$ sudo dpkg -i strace_4.21-1ubuntu1_amd64.deb
```
4. **Verify Installation**:
```
secmancer@htb[/htb]$ strace -h
```


#### Optional Exercise
- **Search for "evil-winrm" Tool on GitHub**: Install it on interactive instances and try different installation methods.
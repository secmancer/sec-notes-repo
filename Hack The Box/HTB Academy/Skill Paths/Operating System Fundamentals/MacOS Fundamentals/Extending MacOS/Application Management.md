### App Store
- To download apps from the App Store, open the **App Store app**, search for the desired app, and click **GET** (for free apps) or the **price** (for paid apps).
- Once downloaded, the app is ready to use.
- To remove an app, go to the **Applications** directory, move it to the **Trash**, and it will be automatically deleted.



### Third-Party Applications
- Applications outside the App Store are usually hosted on the vendor's website. After paying any required fees (if applicable), we can download the application bundle.
- For example, to install **Google Chrome**, search for "Google Chrome Download," and the website will navigate to the appropriate download page.
- Once downloaded, open the application bundle to see its content.
- **Installation Methods:**
	1. **Drag-and-Drop:**
	    - Some applications, like **Chrome**, allow us to drag the bundled application into the **Applications** folder to install it.
	2. **Installer-Based:**
	    - Applications like **Adobe CC** or **Microsoft Office** use an installer to manage multiple applications and configurations.
	    - These applications usually include a bundled uninstaller to ensure complete removal, as moving them to the **Trash** may leave residual files.



### Homebrew
- [Homebrew](https://brew.sh) is a free and open-source package manager used for macOS systems and is an essential tool for developers or penetration testers using macOS. 
- It allows easy installation of many standard tools without the hustle of manually compiling open-source tools or downloading their requirements. 
- For example, `php` used to come built-in with macOS but has been removed from recent versions for 'security concerns'. 
- Installing `php` without Homebrew requires the manual compilation of the `php` tool, which can take some time and be quite problematic. 
- This is why PHP [officially recommends using Homebrew](https://www.php.net/manual/en/install.macosx.packages.php) to install it on recent versions of macOS. The same applies to many other developer tools.
- To install Homebrew, we can follow the instructions found [on their website](https://brew.sh) and execute the following command:
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
- Once the command finishes, we can confirm that Homebrew was successfully installed by running the following command:
```
secmancer@htb[/htb]$ brew -v

Homebrew 3.3.16
Homebrew/homebrew-core
Homebrew/homebrew-cask
```

> **Note:** You may need to close and re-open your terminal before running the above command for the `PATH` to update and have `brew` as part of it.

- Homebrew works similarly to most Linux package managers. 
- For example, we can install `php` by running the following command:
```
brew install php
```
- This command will download and install PHP and all its requirements, and we should be able to use `php` once installed. 
- We can also uninstall PHP by using the `brew uninstall` command. 
- If we want to search for a specific package, then we can use the `brew search` command as follows:
```
secmancer@htb[/htb]$ brew search firefox
==> Formulae
firefoxpwa

==> Casks
firefox			homebrew/cask-versions/firefox-beta					homebrew/cask-versions/firefox-esr
multifirefox	homebrew/cask-versions/firefox-developer-edition	homebrew/cask-versions/firefox-nightly
```
- Most common Linux CLI tools can be installed on macOS through Homebrew, like `wget`, `git`, `tmux`, `node`, `jq`, and many others. 
- Most of them have also been updated to support Apple Silicon chips.
- Homebrew also comes bundled with `Homebrew Cask`, which allows us to install `GUI` applications through Homebrew. 
- Many tools officially provide Casks for their applications, including `Firefox`, `Microsoft Office` suite, and many other popular applications.
- We can install any `Cask` application by adding the `--cask` flag, as follows:
```
brew install firefox --cask
```
- Once installed, the application should show in our applications directory, just like any other application. Homebrew is not the only package manager for macOS, as there are others like [MacPorts](https://www.macports.org). 
- However, Homebrew is the most popular among them and contains the majority of the tools that we may need.



### macOS for Pentesting
- Mac computers are favored by developers and security experts for their versatility and security. Many pentesting tools have macOS-compatible versions, reducing the need for dual boot or VMs.
- To set up a VM, install virtualization software such as [VMWare](https://www.vmware.com/uk/products/fusion.html), [Parallels](https://www.parallels.com/), or [VirtualBox](https://www.virtualbox.org/wiki/Mac%20OS%20X%20build%20instructions). Then download the desired OS ISO and follow installation instructions.
- Using a VM for pentesting is recommended to sandbox potentially harmful activities, safeguarding the macOS host. The VM can be easily reset if compromised.
- Certain pentesting tools can be installed directly on macOS for improved performance when safe to do so.
- **Common macOS-compatible pentesting tools:**
	- [Nmap](https://nmap.org/book/inst-macosx.html)
	- [Burp Suite](https://portswigger.net/burp/documentation/desktop/getting-started/mac-installer)
	- [PowerShell](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell-on-macos?view=powershell-7.3)
	- [Ghidra](https://ghidra-sre.org)
	- [VSCode](https://code.visualstudio.com/docs/setup/mac)

- **Using `Homebrew` to install tools:**
	- [Nmap](https://formulae.brew.sh/formula/nmap#default)
	- [Burp Suite](https://formulae.brew.sh/formula/burp#default)
	- [PowerShell](https://formulae.brew.sh/cask/powershell#default)
	- [Ghidra](https://formulae.brew.sh/cask/ghidra#default)
	- [VSCode](https://formulae.brew.sh/cask/visual-studio-code#default)
	- [SQLMap](https://formulae.brew.sh/formula/sqlmap#default)
	- [VirtualBox](https://formulae.brew.sh/cask/virtualbox#default)



### Questions
- Search 'homebrew' for 'tmux', and one of the results ends in 'nator'. What is the full name of this package?
	- tmuxinator
### App Store
- To download applications from the App Store, we can open the App Store app (found under the Apple logo on the top-left of our screen) and search for the app we are looking for. 
- Then, we can click on `GET` (for free apps) or the `price` (for paid apps) to get the app. Once it downloads, we can start using it.
- To remove any application, go to the applications directory and move it to the `Trash`, and it will be automatically deleted.

### Third-Party Applications
- As for applications outside the app store, each vendor usually hosts their applications on their website and then allows us to download the application bundle once we pay its fees (if paid). - 
- For example, let's try to install `Google Chrome` on our macOS system. To do so, we can search for `Google Chrome Download`, and the vendor's website is usually intelligent enough to navigate us to the download page that matches our operating system.
- Once the application bundle is downloaded, we can open it to see its content. There are two common methods vendors use to install their applications.
- The first method is by providing us with the bundled application, so we can copy it to our applications folder by dragging it to the folder below it and then can start using it, as is the case with Chrome.
- Some other vendors, like Adobe CC or Microsoft Office, need to install several applications simultaneously, along with additional requirements and configurations. 
- So, they provide us with an installer, and then we need to follow the installation window to have their application installed. If an application is installed this way, it usually comes with a bundled uninstaller, as simply moving it to the Trash may not delete all of its content.


### Homebrew
- [Homebrew](https://brew.sh) is a free and open-source package manager used for macOS systems and is an essential tool for developers or penetration testers using macOS. 
- It allows easy installation of many standard tools without the hustle of manually compiling open-source tools or downloading their requirements. For example, `php` used to come built-in with macOS but has been removed from recent versions for 'security concerns'. 
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

- Homebrew works similarly to most Linux package managers. For example, we can install `php` by running the following command:
```
brew install php
```
- This command will download and install PHP and all its requirements, and we should be able to use `php` once installed. 
- We can also uninstall PHP by using the `brew uninstall` command. If we want to search for a specific package, then we can use the `brew search` command as follows:
```
secmancer@htb[/htb]$ brew search firefox
==> Formulae
firefoxpwa

==> Casks
firefox			homebrew/cask-versions/firefox-beta					homebrew/cask-versions/firefox-esr
multifirefox	homebrew/cask-versions/firefox-developer-edition	homebrew/cask-versions/firefox-nightly
```
- Most common Linux CLI tools can be installed on macOS through Homebrew, like `wget`, `git`, `tmux`, `node`, `jq`, and many others. Most of them have also been updated to support Apple Silicon chips.
- Homebrew also comes bundled with `Homebrew Cask`, which allows us to install `GUI` applications through Homebrew. 
- Many tools officially provide Casks for their applications, including `Firefox`, `Microsoft Office` suite, and many other popular applications.
- We can install any `Cask` application by adding the `--cask` flag, as follows:
```
brew install firefox --cask
```
- Once installed, the application should show in our applications directory, just like any other application. Homebrew is not the only package manager for macOS, as there are others like [MacPorts](https://www.macports.org). 
- However, Homebrew is the most popular among them and contains the majority of the tools that we may need.


### macOS for Pentesting
- Mac computers are very popular with developers and security experts alike, and this is largely due to their versatility and security. While many users set up another Operating System, like Linux or Windows, through Virtual Machines or dual boot, many of the most common pentesting tools also have versions that run directly on macOS.
- We can set up a VM by installing a virtualization software like [VMWare](https://www.vmware.com/uk/products/fusion.html), [Parallels](https://www.parallels.com/), or [VirtualBox](https://www.virtualbox.org/wiki/Mac%20OS%20X%20build%20instructions), and then download the ISO for the OS we want and follow the instructions to install it. The instructions of installing an OS as a VM are explained in the [Setting Up](https://academy.hackthebox.com/module/details/87) module and are fairly similar to do so on macOS as well. Once we have the Linux/Windows setup, then we can set that operating system for pentesting, as was also explained in the [Setting Up](https://academy.hackthebox.com/module/details/87) module as well.
- It is recommended to use a VM as the main host for your pentesting exercises, not only because you can have it fully set up with pentesting tools, but also because this limits all of your pentesting exercises within a sandboxed VM, and avoids potentially causing any harm to your main OS 'macOS'. Pentesting may include sensitive activities or dealing with potentially harmful malware, and so it is best to have all of that sandboxed within a VM that you can delete and reinstall in case it gets damaged.
- Still, some pentesting tools may be quite safe to have installed directly on macOS, especially if you use them often, as this may give a significant increase in their performance when compared to running them within a VM.
- We already have most of the scripting languages bundled with macOS, like bash or python. Some of the common pentesting tools with macOS versions include:
	- [Nmap](https://nmap.org/book/inst-macosx.html)
	- [Burp Suite](https://portswigger.net/burp/documentation/desktop/getting-started/mac-installer)
	- [PowerShell](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell-on-macos?view=powershell-7.3)
	- [Ghidra](https://ghidra-sre.org)
	- [VSCode](https://code.visualstudio.com/docs/setup/mac)
- Furthermore, all of the above tools and many others may also be installed directly with `Homebrew`, such as:
	- [Nmap](https://formulae.brew.sh/formula/nmap#default)
	- [Burp Suite](https://formulae.brew.sh/formula/burp#default)
	- [PowerShell](https://formulae.brew.sh/cask/powershell#default)
	- [Ghidra](https://formulae.brew.sh/cask/ghidra#default)
	- [VSCode](https://formulae.brew.sh/cask/visual-studio-code#default)
	- [SQLMap](https://formulae.brew.sh/formula/sqlmap#default)
	- [Virtual Box](https://formulae.brew.sh/cask/virtualbox#default)

### Questions
- Search 'homebrew' for 'tmux', and one of the results ends in 'nator'. What is the full name of this package?
	- tmuxinator
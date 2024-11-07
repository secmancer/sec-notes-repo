### Application Security Considerations
- As discussed in the previous section, macOS, like any other operating system, provides multiple ways of installing new software on the OS. 
- For most use cases, we can stick to Apple's recommended option of `App Store` (and) `Identified Developers`, which is a setting we can find in `System Settings`>`Privacy & Security`, which would allow installing applications as shown in the previous section. 
- Let's see the security implication of each use case.
- Sticking to the first option of only allowing apps to be installed from the `App Store` dramatically increases the operating system's security and substantially reduces the chances of malware being installed on our operating system. 
- This is because the operating system would prevent any other type of executables from being executed or installed if they were not originating from the App Store and were signed and approved directly by Apple.

### Identified Developers
- Professional users of macOS may not find some of the applications they require on the App Store and hence need to download and install them from the vendor's website manually. 
- This is why Apple also allows the option of installing applications signed by `Identified Developers`. Such applications have certificates to sign their applications that are [provided by Apple to trusted vendors](https://support.apple.com/en-us/HT209143), like Google, Microsoft, Adobe, and many others. 
- This way, we can safely install third-party software without solely relying on the App Store.
- To ensure only safe software can run on the system, macOS has a feature called [Gatekeeper](https://support.apple.com/en-us/HT202491) that acts as a protection agent, detecting and blocking malware and other malicious extensions or applications. 
- It works alongside File quarantining and code signing to ensure the integrity of the system resources.

### Unidentified Developers
- Sometimes, we may download an application, and Gatekeeper will warn us that `the application is from an unidentified developer`, and will not open the application and recommend moving it to trash.
- Even though this can be bypassed by going to the earlier mentioned setting and clicking on `Open anyway`, we strongly recommend not opening or installing this application from the web, as its origin and security cannot be trusted.
- This is why we recommend never installing cracked or patched applications. Such applications may also have backdoors added to them or may execute code upon running them to install persistent malware on our operating system.


### Auto Updates
- Auto-updates play a critical role in keeping our operating system and applications safe by constantly and automatically providing patches for known vulnerabilities. 
- This is why it is strongly recommended to enable `Auto Updates` for our macOS system and all of our third-party applications. To allow auto-updates for macOS and App Store apps, we can go to `System Settings`>`General`>`Software Update` and then check `Automatic Updates` or `Automatically keep my Mac up to date`. -
- We should also click on `Advanced` and ensure that everything is checked.
- As for third-party applications, each has a different method for updating its applications. 
- However, Apple usually requires vendors to enable auto-updates by default, so most third-party applications should be automatically updated.


### macOS Built-in Security
- MacOS is built to be secure by design, which is why many security settings and configurations are enabled by default. 
- Let's go through some of the main security features availble in macOS and how we can configure them.
- Security measures always come at the cost of convenience, which is why we frequently see apps asking us for permission to use a specific macOS feature, like our camera, microphone, or clipboard. 
- All of these security settings can be found under `System Settings`>`Privacy & Security`.
- You will not need to manually configure these settings, as each application will ask for its privileges on first use, just like the case is on an iPhone. This may be somewhat inconvenient, as we mentioned earlier, but this dramatically enhances the security of your system.
- If one of the applications is malicious or gets exploited, it will not get access to the entire system but will be sandboxed and will only get access to privileges you allow.
- For example, the macOS version of the popular application `Zoom` [had a vulnerability](https://objective-see.org/blog/blog_0x56.html) that enables attackers to access the target's webcam. 
- However, this only works because the application was granted access to the webcam; otherwise, the attacker would not be able to access the target's webcam.
- From time to time, you may want to double-check or review which applications have access to which privileges. The most sensitive settings to check are:
	- Camera
	- Microphone
	- Input monitoring
	- Full Disk Access/Files and Folders
	- Screen recording
- Even though these permissions should restrict your applications from accessing system-wide features, some recent zero-day macOS vulnerabilities have allowed attackers to escape the application sandbox and bypass the access control and privacy restrictions to access system-wide features, even if the application did not have these permissions. 
- This is why keeping the OS and all applications up to date is always recommended.

### FireVault
- Under `System Settings`>`Privacy & Security`, we can turn on `FileVault`, which enables disk encryption for the macOS system. 
- We strongly recommend turning it on to ensure data cannot be extracted from the system without a password. This setting is on by default on modern Apple Silicon hardware.


### Firewall
- We can enable an internet `Firewall` either in the `Firewall` tab under `System Preferences`>`Security and Privacy` on macOS 12 or earlier or in the `System Settings`>`Network` on macOS 13 or newer.
- The firewall settings automatically allow connections for the built-in and trusted applications, so turning on the firewall should not affect your general use of the system. Sometimes, it may ask you to allow a specific application through the firewall, like VPN connections or proxy applications (e.g., Burp Suite). 
- An internet firewall may help prevent malicious software from remotely controlling our machine or being able to connect back to its command and control center, so using it is very recommended.


### Keychain
- One of the most important aspects of any system is how it handles saving our passwords. It is always recommended to use a different complex password for each application we use, which makes it impossible for us to remember all of them. 
- This is necessary if any of our online accounts are compromised and our password is leaked; then, we will not need to change our passwords in all of our online accounts but will only need to change the password of that compromised account.
- So, we need our operating system or a third-party application to handle that for us, and macOS provides this through `Keychain`, which can be accessed through the `Keychain Access` app or under `System Settings`>`Passwords` in recent macOS versions.
- Keychain allows us to generate a random complex password when creating a new account in any app or web application, and then saves it for future use and syncs all of our passwords across our other Apple devices. 
- Furthermore, it also allows us to save our credentials when logging into any app or web application and auto-fills it whenever we need to log into that app in the future. This makes it very convenient to stay secure online without needing a third-party application to handle all of this for us, especially with some of these third-party applications not being as secure as macOS.
- In recent macOS releases, Keychain also allows us to store our two-factor authentication (2FA) keys with our passwords. It can automatically fill in the code when logging into the app, which makes it very convenient to be secure by enabling 2FA without any extra complications.
- MacOS 13 also introduced the new open standard for password-less login '`passkeys`', which does not store any form of password on the website or rely on any form of password. 
- This prevents the possibility of leaking or phishing users' passwords, as no password is being used at all.
- Another helpful feature of Keychain is detecting any weak or repeated passwords we may use and prompting us to change them to more secure ones. 
- It also automatically checks if our login email address is found in any of the online leaked password databases. 
- If it finds that our credentials have been compromised, it will notify us and prompt us to change that password.

### Find My Mac
- MacOS has other built-in security and privacy features that help keep you safe online. One such feature is `Find My Mac`, which you can turn on by going to `System Settings`>`Apple ID` and then checking `Find My Mac`. 
- This allows you to locate your MacBook in case it gets stolen, and it should even work if the device is offline and not connected to the internet. 
- Furthermore, if you suspect that your device has been stolen, you will also have the option to lock it or erase it remotely. If you mark the device as `stolen`, it will prevent it from being sold or used by another user.

### iCloud Private Relay
- Recent macOS versions also have the [iCloud Private Relay](https://support.apple.com/en-gb/HT212614) feature, which you can turn on at the same above screen. Private relay works as a built-in VPN service, encrypts your internet traffic and browsing history, and hides your public IP. 
- This is incredibly important for securing your online presence and can help reduce the number of scams and spam you receive and keep your online activity private from prying eyes. 
- Private relay also uses two hops to encrypt your traffic, so no one (not even Apple) has complete visibility over your online activity.
- However, this comes with disadvantages, like lower internet speed or showing incorrect locations for some websites. 
- It is also still in 'beta' as of writing this module and does interfere with some remote services, like `Git` and `Docker`, so some developers may not want to use it.


### Hide My Email
- Another similar feature Apple recently introduced is [Hide My Email](https://support.apple.com/en-gb/guide/mail/mlhl47c969f8/mac), which allows us to create single-use email aliases that forward to our real email address. 
- This allows us to use them with online services and various applications that require an email address for registration without enrolling into their -often spam- mailing list. 
- Once we are done with any service, we can delete the email alias, and they will no longer receive emails or forward them to our email address.
- `Hide My Email` may also be turned on in the Apple ID tab, just like Find My Mac.


### Advanced Data Protection
- MacOS allows us to sync most of our data over the cloud and even provides iCloud Drive to be used as cloud data storage. 
- However, even though cloud storage offers a seamless experience for data storage and sharing, it comes at the cost of data privacy. 
- It must be noted that most cloud storage providers today do not support end-to-end encryption, so our data can be extracted by these vendors if required by the law and, in some cases, can be used as test data to train AI machines.
- By default, services like iCloud Keychain and payment card information are end-to-end encrypted, while others like iCloud Drive and iCloud photos are not. 
- This is so Apple can restore data if we forget our iCloud password; otherwise, we would risk completely losing our cloud-stored data if we forget our passwords since the data would be encrypted with our passwords, and Apple won't have any other means of decrypting these files. 
- However, Apple [recently announced](https://www.apple.com/newsroom/2022/12/apple-advances-user-security-with-powerful-new-data-protections/) that it is adding the option to enable end-to-end encryption to all data stored in iCloud, which is fantastic news for our privacy. 
- This way, we can trust cloud storage for our sensitive files, though this would mean that we would take responsibility for data loss if we ever forget our password and lose access to our [recovery key/contact](https://support.apple.com/en-us/HT212520).


### Lockdown Mode
- MacOS 13 'Ventura' and iOS 16 added a very powerful first-of-its-kind security feature called [Lockdown Mode](https://support.apple.com/en-gb/HT212650). 
- Lockdown Mode is a very 'locked' version of macOS, where most unnecessary services are disabled, and many other services are limited, like messaging or online browsing, along with preventing the use of most third-party applications. 
- This, along with many other precautions, is done to prevent targetting 'high importance' users by powerful threat actors using sophisticated cyber attacks, like macOS 0-days.
- If ever needed, we can turn on/off Lockdown Mode in `System Settings`>`Privacy & Security`. It is vital to remember that most people may never need to turn on this feature, as such sophisticated cyber attacks are very expensive to develop and deploy. 
- As such only "high-importance" individuals are targeted in these types of attacks.


### KnockKnock
- [Objective See](https://objective-see.org) is a non-profit foundation that creates free, open-source macOS security tools. They provide many excellent security tools that help us detect malware and monitor macOS against breaches.
- One of their most common tools is [KnockKnock](https://objective-see.org/products/knockknock.html), which scans all locations where persistent malware is most likely to reside and checks them for malware. If any malware is found, it will prompt you to delete it. [BlockBlock](https://objective-see.org/products/blockblock.html) plays a similar role but actively monitors these locations and requires approval for any installation on these persistent directories.


### Netiquette
- Another helpful tool is [Netiquette](https://objective-see.org/products/netiquette.html), which shows all active outgoing and incoming connections, and checks each for common malware. [LuLu](https://objective-see.org/products/lulu.html) also plays a similar role by actively monitoring connections and prompts you whenever an application attempts to open a new connection.
- The active monitoring tools give you a higher level of control and security but may be very inconvenient as they will keep prompting you for many types of tasks, especially if you are a developer. 
- So, you may want to use [KnockKnock](https://objective-see.org/products/knockknock.html) and [Netiquette](https://objective-see.org/products/netiquette.html) for periodic manual checks, and if you need that next level of security, then you may use the other two. 
- You can also check [Objective See](https://objective-see.org)'s website for their other tools, like [TaskExplorer](https://objective-see.org/products/taskexplorer.html) that reviews runnings applications for malware or [RansomWhere?](https://objective-see.org/products/ransomwhere.html) which prevents ransomware from encrypting your files.

> **Tip:** You may also use macOS's native Activity Monitor "search for it via Spotlight" to view/kill any running processes and examine their resource usage. There are also many applications that provide a drop-down menu to monitor macOS resources and processes, like [iStat Menus](https://bjango.com/mac/istatmenus/) or [CleanMyMac](https://macpaw.com/cleanmymac).
### Application Security Considerations
- As discussed earlier, macOS provides several ways to install new software, with the **App Store** and **Identified Developers** being the most common methods. These options are found under **System Settings > Privacy & Security**, allowing you to control where apps can be installed from.
- The security implications of each method are significant.
- Sticking with the **App Store** installation method **dramatically increases** the operating system's security. This is because only apps that are signed, verified, and approved by Apple are allowed, reducing the risk of malware or unauthorized software.
- This approach **prevents the execution** or installation of any executables that do not originate from the App Store, making it one of the safest methods to install software on macOS.



### Identified Developers
- Professional macOS users may occasionally need to install applications that are not available on the App Store. In such cases, Apple provides the option to install software signed by **Identified Developers**.
- **Identified Developers** are trusted vendors, such as Google, Microsoft, and Adobe, who are issued certificates by Apple to sign their applications. This allows us to safely install third-party software without having to rely solely on the App Store.
- To further enhance security, macOS employs a feature called **Gatekeeper**, which acts as a protective agent. Gatekeeper detects and blocks potential malware or malicious applications.
- Gatekeeper works in conjunction with **file quarantining** and **code signing**, ensuring the integrity of the system and preventing the execution of potentially harmful software.



### Unidentified Developers
- Sometimes, when downloading an application, **Gatekeeper** may warn us that the application is from an **unidentified developer** and will prevent it from opening. It will recommend moving the application to trash.
- Although this warning can be bypassed by going to **System Settings** > **Privacy & Security** and clicking on **Open Anyway**, we strongly recommend **not opening or installing** such applications, as their origin and security cannot be verified.
- We advise against installing **cracked** or **patched applications**, as they may contain hidden backdoors or malicious code that could compromise the system. These applications may execute harmful actions upon running, such as installing persistent malware on the operating system.



### Auto Updates
- **Auto-updates** are crucial for maintaining the security of both our operating system and applications by ensuring they receive timely patches for known vulnerabilities.
- It is strongly recommended to enable **Auto Updates** for both macOS and third-party applications. To enable auto-updates for macOS and **App Store** apps, navigate to **System Settings** > **General** > **Software Update**, and check **Automatic Updates** or **Automatically keep my Mac up to date**.
- Additionally, click on **Advanced** and ensure that all available options are checked to allow full auto-update functionality.
- For third-party applications, each may have a different method for enabling updates. However, Apple typically requires developers to enable auto-updates by default, so most third-party apps should update automatically without manual intervention.



### macOS Built-in Security
- macOS is designed with security in mind, with many security features enabled by default to protect users from potential threats.
- The **Privacy & Security** section in **System Settings** is where most of these security measures can be configured, and it allows users to manage permissions for system features like the camera, microphone, and clipboard.
- Security features often come with a trade-off in convenience, which is why apps may ask for permission to access certain features upon first use, much like on an iPhone. While this can feel inconvenient, it significantly enhances security by limiting what applications can access.
- If an app is malicious or gets exploited, it will not have unrestricted access to your entire system. Instead, it is sandboxed and only granted the specific privileges you allow.
- For example, the **Zoom** app for macOS had a vulnerability that allowed attackers to access the webcam, but only if the app had been granted access to the webcam in the first place. Without that permission, the attacker could not gain access.
- To review or double-check which apps have access to sensitive system features, you can visit **System Settings** > **Privacy & Security** and look at the following key permissions:
    - Camera
    - Microphone
    - Input monitoring
    - Full Disk Access/Files and Folders
    - Screen recording
- While these permissions help to limit app access to system resources, recent **zero-day vulnerabilities** in macOS have occasionally allowed attackers to bypass these restrictions. Therefore, it's essential to keep both the macOS system and applications up to date to mitigate these risks.



### FireVault
- Under `System Settings`>`Privacy & Security`, we can turn on `FileVault`, which enables disk encryption for the macOS system. 
- We strongly recommend turning it on to ensure data cannot be extracted from the system without a password. 
- This setting is on by default on modern Apple Silicon hardware.



### Firewall
- We can enable an internet `Firewall` either in the `Firewall` tab under `System Preferences`>`Security and Privacy` on macOS 12 or earlier or in the `System Settings`>`Network` on macOS 13 or newer.
- The firewall settings automatically allow connections for the built-in and trusted applications, so turning on the firewall should not affect your general use of the system. 
- Sometimes, it may ask you to allow a specific application through the firewall, like VPN connections or proxy applications (e.g., Burp Suite). 
- An internet firewall may help prevent malicious software from remotely controlling our machine or being able to connect back to its command and control center, so using it is very recommended.



### Keychain
- One of the most important aspects of system security is how passwords are managed, especially since it’s recommended to use a unique, complex password for every application. This helps protect our accounts in case one is compromised, as we only need to change the password for the affected account, not for all of them.
- macOS provides a built-in solution for this through **Keychain**, which securely stores passwords and credentials for apps and websites. Keychain can be accessed via the **Keychain Access** app or through **System Settings** > **Passwords** in recent macOS versions.
- **Keychain** can automatically generate random, complex passwords when creating new accounts and saves them for future use. It also syncs passwords across all Apple devices, making it easy to access them securely.
- When logging into apps or websites, Keychain can auto-fill your credentials, which saves time and ensures you don’t need to remember every password. This built-in feature eliminates the need for third-party password managers, some of which may not be as secure as macOS.
- **Keychain** also supports storing two-factor authentication (2FA) keys, and it can auto-fill the 2FA code when logging into apps. This makes it more convenient to secure accounts with 2FA without any extra effort.
- In macOS 13, Apple introduced the open standard for password-less login, known as **passkeys**. This method eliminates the need to store passwords on websites or rely on passwords at all, reducing the risk of passwords being leaked or phished.
- **Keychain** can also detect weak or reused passwords and alert users to change them. Additionally, it checks if your login email has been found in any known leaked password databases. If your credentials are compromised, Keychain will notify you and prompt you to change your password.



### Find My Mac
- MacOS has other built-in security and privacy features that help keep you safe online. 
- One such feature is `Find My Mac`, which you can turn on by going to `System Settings`>`Apple ID` and then checking `Find My Mac`. 
- This allows you to locate your MacBook in case it gets stolen, and it should even work if the device is offline and not connected to the internet. 
- Furthermore, if you suspect that your device has been stolen, you will also have the option to lock it or erase it remotely.
- If you mark the device as `stolen`, it will prevent it from being sold or used by another user.



### iCloud Private Relay
- Recent macOS versions include the **iCloud Private Relay** feature, which can be enabled in the same **System Settings** > **Privacy & Security** screen. Private Relay functions like a built-in VPN, encrypting your internet traffic and browsing history while hiding your public IP address.
- This feature is crucial for securing your online presence, helping to reduce spam and scams, and ensuring that your online activities remain private from prying eyes.
- Private Relay uses a two-hop architecture to encrypt your traffic, which means no one (not even Apple) can fully access or monitor your online activities.
- However, there are some drawbacks to using Private Relay. It may reduce internet speed, and certain websites may incorrectly detect your location.
- Additionally, as of writing, iCloud Private Relay is still in beta and can interfere with some services, such as **Git** and **Docker**, which may be a concern for developers who rely on these tools.



### Hide My Email
- Another similar feature Apple recently introduced is [Hide My Email](https://support.apple.com/en-gb/guide/mail/mlhl47c969f8/mac), which allows us to create single-use email aliases that forward to our real email address. 
- This allows us to use them with online services and various applications that require an email address for registration without enrolling into their -often spam- mailing list. 
- Once we are done with any service, we can delete the email alias, and they will no longer receive emails or forward them to our email address.
- `Hide My Email` may also be turned on in the Apple ID tab, just like Find My Mac.



### Advanced Data Protection
- macOS allows seamless synchronization of most data over the cloud, with **iCloud Drive** serving as the primary cloud data storage solution. While cloud storage offers convenience for data access and sharing, it also introduces concerns about **data privacy**.
- It's important to note that most cloud storage providers, including Apple, do not support **end-to-end encryption** by default for all data. This means that, in certain situations, cloud service providers could be required by law to hand over your data, or use it for other purposes, such as training AI models.
- By default, sensitive data like **iCloud Keychain** and **payment card information** are **end-to-end encrypted** to protect user privacy. However, services such as **iCloud Drive** and **iCloud Photos** do not have this level of encryption by default. This is to allow Apple to recover data if a user forgets their iCloud password. Without this access, you could risk permanently losing your cloud-stored data if it's encrypted with your password and no other decryption method is available.
- However, Apple has recently announced [enhanced privacy measures](https://www.apple.com/newsroom/2022/12/apple-advances-user-security-with-powerful-new-data-protections/) that provide users with the option to enable **end-to-end encryption** for all iCloud data. This is a significant step toward improving data privacy, as it ensures that even Apple cannot access your sensitive files.
- While this enhanced security feature provides an added layer of privacy, it also means users take on more responsibility. If you forget your password and lose access to your **recovery key** or contact, your data could become irretrievable. Therefore, it’s essential to safeguard your recovery information carefully.



### Lockdown Mode
- MacOS 13 'Ventura' and iOS 16 added a very powerful first-of-its-kind security feature called [Lockdown Mode](https://support.apple.com/en-gb/HT212650). 
- Lockdown Mode is a very 'locked' version of macOS, where most unnecessary services are disabled, and many other services are limited, like messaging or online browsing, along with preventing the use of most third-party applications. 
- This, along with many other precautions, is done to prevent targetting 'high importance' users by powerful threat actors using sophisticated cyber attacks, like macOS 0-days.
- If ever needed, we can turn on/off Lockdown Mode in `System Settings`>`Privacy & Security`.
- It is vital to remember that most people may never need to turn on this feature, as such sophisticated cyber attacks are very expensive to develop and deploy. 
- As such only "high-importance" individuals are targeted in these types of attacks.



### KnockKnock
- [Objective See](https://objective-see.org) is a non-profit foundation that creates free, open-source macOS security tools. 
- They provide many excellent security tools that help us detect malware and monitor macOS against breaches.
- One of their most common tools is [KnockKnock](https://objective-see.org/products/knockknock.html), which scans all locations where persistent malware is most likely to reside and checks them for malware. 
- If any malware is found, it will prompt you to delete it. [BlockBlock](https://objective-see.org/products/blockblock.html) plays a similar role but actively monitors these locations and requires approval for any installation on these persistent directories.



### Netiquette
- Another helpful tool is [Netiquette](https://objective-see.org/products/netiquette.html), which shows all active outgoing and incoming connections, and checks each for common malware.
- [LuLu](https://objective-see.org/products/lulu.html) also plays a similar role by actively monitoring connections and prompts you whenever an application attempts to open a new connection.
- The active monitoring tools give you a higher level of control and security but may be very inconvenient as they will keep prompting you for many types of tasks, especially if you are a developer. 
- So, you may want to use [KnockKnock](https://objective-see.org/products/knockknock.html) and [Netiquette](https://objective-see.org/products/netiquette.html) for periodic manual checks, and if you need that next level of security, then you may use the other two. 
- You can also check [Objective See](https://objective-see.org)'s website for their other tools, like [TaskExplorer](https://objective-see.org/products/taskexplorer.html) that reviews runnings applications for malware or [RansomWhere?](https://objective-see.org/products/ransomwhere.html) which prevents ransomware from encrypting your files.

> **Tip:** You may also use macOS's native Activity Monitor "search for it via Spotlight" to view/kill any running processes and examine their resource usage. There are also many applications that provide a drop-down menu to monitor macOS resources and processes, like [iStat Menus](https://bjango.com/mac/istatmenus/) or [CleanMyMac](https://macpaw.com/cleanmymac).
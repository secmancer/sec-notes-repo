### What is macOS
- Operating system used in Apple's iMac/Macbook product line
- Widely used, second largest in market share (behind Windows)
- Seen in daily home use, business management, graphical design, and the arts



### Timeline
- 2000-2002
	- Fall 2000: public beta named Kodiak
	- Spring 2001
		- Mac OS X 10.0 (Cheetah)
			- First visual of the new UI Aqua
		- Mac OS X 10.1 (Puma)
			- Improved system performance, replaced Mac OS 9 on a large amount of Mac computers
	- Fall 2002: Mac OS X 10.2 (Jaguar)
		- User interaction improvements
		- New applications like iChat
- 2003
	- Fall: OS X 10.3 (Panther)
		- New web browser Safari introduced
		- Support for Active Directory
- 2005
	- OS X 10.4 (Tiger)
		- New look, widgets, and dashboards
		- Initial Intel-based chipset support
- 2007-2009
	- Spring 2007: iPhone and iOS is first released
	- Fall 2007: OS X 10.5 (Leopard)
		- Added a new built-in backup system, called Time Machine
		- 64-bit support
		- Boot Camp support, allows Windows OS dual booting
	- 2009: OS X 10.6 (Snow Leopard)
		- AppleStore added
		- PowerPC processors dropped for support
- 2011-2012
	- 2011: OS X 10.7 (Lion)
		- Some iOS features rolled over
		- Gestures
		- Saved window states
		- Introduction of iCloud
	- 2012: OS X 10.8 (Mountain Lion)
		- More iOS features rolled over
- 2013
	- Yearly release cycle
	- California landmark based names instead of big cats
	- OS X 10.9 (Mavericks)
		- All future releases will be free
		- Some functionality tweaks
- 2014-2015:
	- OS X 10.10 (Yosemite)
		- Handoff functionality
		- new UI
	- OS X 10.11 (El Capitan)
		- Performance changes
		- Ability to tile the screen with split views
- 2016-2017
	- OS X renamed to macOS
		- macOS 10.12 (Sierra)
			- Siri integration
			- Apply Pay
	- macOS 10.13 (High Sierra)
		- Switch to Apple File System (APFS)
- 2018
	- macOS 10.14 (Mojave)
		- Visual enhancements
		- Dark mode
		- Additional iOS apps ported
- 2019
	- macOS 10.15 (Catalina)
		- iTunes split into three seperate apps
			- Apple TV, Podcasts, Music
		- More iOS features integrated
		- Secondary display feature with an iPad (Sidecar)
- 2020
	- macOS 11 (Big Sur)
		- UI changes
		- Improved communication channel
		- Initial Apple Silicon support
- 2021
	- macOS 12 (Monterey)
		- Universal Control introduction
		- Airplay changes
		- Spatial Audio added
- 2022
	- macOS 13 (Ventura)
		- Most recent at the time of writing
		- Stage Manager added, a new window management tool
		- Continuity Camera implemented



### OS + Arch
- Kernel: XNU
	- The Mach kernel is the basis (along with portions from BSD) of the macOS and iOS `XNU` Kernel architecture, which handles our memory, processors, drivers, and other low-level processes.
- OS Base: Darwin
	- FreeBSD derivative open sourced by Apple
	- Darwin is the base of the macOS operating system. Apple has released Darwin for open-source use. Darwin, combined with several other components such as `Aqua`, `Finder`, and other `custom components`, make up the macOS as we know it.
- Supports:
	- Apple Silicon
	- Intel (for now, planned deprecation)



### Core Elements
- GUI: Aqua
	- Basis for the Graphical interface and visual theme for macOS. As technology has advanced, so has Aqua, providing more and more support for other displays, rendering technologies, and much more. It is known for its flowy style, animations, and transparency with windows and taskbars.
- File Manager: Finder
	- Component of macOS that provides the Desktop experience and File management functions within the OS. Aqua is also responsible for the launching of other applications.
- Application Sandbox
	- By default, macOS and any apps within it utilize the concept of sandboxing, which restricts the application's access outside of the resources necessary for it to run. This security feature would limit the risk of a vulnerability to the application itself and prevent harm to the macOS system or other files/applications within it.
- Cocoa
	- Application management layer and API used with macOS. It is responsible for the behavior of many built-in applications within macOS. Cocoa is also a development framework made for bringing applications into the Apple ecosystem. Things like notifications, Siri, and more, function because of Cocoa.



### Questions
- What BSD derivative is the basis of the macOS operating system?
	- Darwin
- What provides the desktop experience and file management capabilities within macOS?
	- Finder

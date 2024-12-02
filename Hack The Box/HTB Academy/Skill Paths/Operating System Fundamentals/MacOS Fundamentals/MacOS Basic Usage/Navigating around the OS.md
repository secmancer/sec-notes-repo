### Using Finder
- As discussed in the previous section, `Finder` is the component of macOS that provides the File management functions within the OS. You can use `Finder` to find and browse files present inside your Mac.

### Viewing the Root Directory
- One way to view the `root` directory is to launch the `Finder` app from the Dock, click on the `Go` Pane at the top, select `Computer` & click on `Storage`.
- Another way to open the root directory is to launch the `Finder` app from Dock; enter the keyboard shortcut `Command + Shift + G`, type `/`, and hit `Go`.
- You may also go up and down directories in Finder using the `Command` with the `up` and `down` arrows.


### Copying and Pasting Files and Folders
- You may copy/paste items in Finder with the right-click menu or the `Command + C` and `Command + V` keyboard shortcuts.
- You can also move items by dragging them from one folder to another or even duplicate any item by holding the `option` key while dragging them.


### Cutting and Pasting Files and Foldres
- MacOS does not offer a direct GUI feature to cut and paste files & folders using `Finder`. But you can use the keyboard shortcut `Command + Option + V` to move the copied file directly.
	1. Launch the `Finder` app from the Dock.
	2. Right-click on the file or folder you want to move and select `Copy`.
	3. Use `Finder` to head to the location where you want to move a file, and use the keyboard shortcut `Command + Option + V` to move the file.
- Another way to move files in macOS is using the `mv` command in the `terminal`, which must be used with caution as it is an irreversible command. 
- To do so, open a terminal from Dock & run the following command to move the `Test` folder from the Users `Document directory` into the Users `Desktop directory`.
```
[root@htb]/Users$ mv /Users/htb-student/Documents/Test /Users/htb-student/Desktop/Test
```

> **Note:** While macOS does not allow "Cut/Paste" of files to avoid potential file loss, it does allow "Cut/Paste" of text through the right-click menu or with the "Command + X" shortcut.


### Viewing Hidden Files and Folders
- There are lots of hidden files and folders present on macOS that prevent users from accidentally deleting files used by the operating system. 
- However, there are multiple ways to view hidden files on a Mac using the GUI and terminal.
- To view hidden files and folders using the GUI:
	1. Open the folder where you want to see hidden files
	2. Hold down `Command + Shift + .` (full stop/period)
	3. You may also change the default view of Finder to show hidden files, as follows:
		1. Open a terminal from `Dock` & run the following commands in Terminal
```
[root@htb]/Users$ defaults write com.apple.Finder AppleShowAllFiles true
[root@htb]/Users$ killall Finder
```


### Preview Pane
- The `Preview Pane` within `Finder` allows us to glance at what files and images look like before opening them. 
- It provides instant previews of what’s in each file you highlight with additional information about the file such as `Creation Date & Time`, `Last Modified Date & Time`, `Last Opened Date & Time`, etc.
- Enable `Preview Pane` inside `Finder` to look at the file preview.
	- 1. Launch the `Finder` app from the Dock.
	- 2. Click on the `View` Pane at the top & select `Show Preview`.
	- 3. Launch the `Finder` app from the Dock.
	- 4. Click on the `View` Pane at the top & select `Show Preview`.


### Spotlight
- `Spotlight` is a `system-wide` desktop search feature of Apple's macOS and iOS operating systems, as discussed in previous sections. `Spotlight` can help you quickly find items present on your Mac.
- Let's try opening a `Dictionary` in macOS using Spotlight.
	1. Click on the `magnifying glass` icon at the top-right corner of the desktop or use the keyboard shortcut (`Command + Space bar`) to open `Spotlight`.
	2. Type the keyword `dictionary` inside the `Spotlight search bar` and click on the `Dictionary` app to open a Dictionary instance.


### Moving Around Applications
- Moving and switching from one app to another can be tedious, especially if there is a frequent need to split apps every few seconds. To improve efficiency while working on multiple apps, macOS provides features like `Mission Control` & `Split View`.


### Mission Control
- MacOS provides a feature named `Mission Control`, which offers a bird's-eye view of all open windows, desktop spaces, and apps, making switching between them easy.
- There are multiple ways to open the `bird's-eye` view on your Mac.
	1. Swipe up using three fingers on your trackpad.
	2. Open the Mission Control app manually from the Launchpad.

### Split View
- By using Split View, you can split your Mac screen between two apps. It would automatically resize the screen without manually moving and resizing windows. 
- Split View only works if you already have two or more apps running in the background.
- To use Split View with apps, hover the mouse pointer over the `full-screen` button (Green Colored) on the `top-left,` and you will be presented with three options to select from:
	1. Enter Fullscreen
	2. Tile Window to Left of Screen
	3. Tile Window to Right of Screen
- Choose `Tile Window to Left of Screen` from the menu, and the window will fill that side of the screen. 
- Now hover the mouse pointer onto the next side of the screen and select another app to begin using both apps in split windows side by side.

### Questions
- Download the above file and double click on it to unzip it. The extracted folder may appear empty, but in reality it has a hidden file with the flag. Can you find the flag?
	- HTB{F1l3s_c@n_Hide}

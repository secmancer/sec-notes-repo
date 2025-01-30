### **Navigating macOS - Notes**
- Navigating macOS efficiently requires understanding **Finder, Spotlight, Mission Control, and Split View**. Below are essential navigation techniques for improved productivity.



### **1. Using Finder (File Manager)**
- **Finder** provides access to **files, folders, and system directories**.
- Can be launched from the **Dock** or via **Command (⌘) + Spacebar > Search "Finder"**.
- #### **View Root Directory**
	1. Open **Finder**.
	2. Click **Go (Menu Bar) > Computer > Storage**.
	3. OR use the shortcut:
    ```bash
    Command (⌘) + Shift + G, type `/`, and press Enter.
    ```
- #### **Navigating Folders**
	- **Move Up a Directory:** `Command (⌘) + Up Arrow`
	- **Move Down a Directory:** `Command (⌘) + Down Arrow`
- #### **Copy & Paste Files/Folders**
	- **Copy:** `Command (⌘) + C`
	- **Paste:** `Command (⌘) + V`
	- **Duplicate (Copy in Same Location):** `Option + Drag`
- #### **Move (Cut & Paste) Files/Folders**
	- macOS **does not support** "Cut" for files in Finder but allows "Move" via:
    ```bash
    Command (⌘) + Option + V  (after copying)
    ```
	- **Using Terminal (mv command)**
    ```bash
    mv /Users/htb-student/Documents/Test /Users/htb-student/Desktop/Test
    ```
- **⚠️ Warning:** The `mv` command is **irreversible** (no undo).



### **2. Viewing Hidden Files & Folders**
- macOS hides system files to prevent accidental deletion.
- #### **Show Hidden Files (Shortcut)**
	1. Open **Finder**.
	2. Press:
    ```bash
    Command (⌘) + Shift + . (Period)
    ```
- #### **Show Hidden Files Permanently (Terminal Command)**
```bash
defaults write com.apple.Finder AppleShowAllFiles true
killall Finder
```
- To **hide again**, replace `true` with `false`.



### **3. Using Preview Pane in Finder**
- The **Preview Pane** provides a **quick preview of files** without opening them.
- #### **Enable Preview Pane**
	1. Open **Finder**.
	2. Click **View (Menu Bar) > Show Preview**.
	3. Click a file to see its preview **on the right side**.



### **4. Finding Files & Apps with Spotlight**
- **Spotlight** is a **system-wide search** feature.
- Shortcut:
    ```bash
    Command (⌘) + Spacebar
    ```
- Example:
    1. Open Spotlight (`Command + Spacebar`).
    2. Type `"Dictionary"`, then select **Dictionary app**.



### **5. Switching Between Apps Efficiently**
- #### **Mission Control (Bird's-Eye View of Open Apps)**
	- **View all open windows & desktops**.
	- Open Mission Control by:
	    - Swiping **up with three fingers** on the **trackpad**.
	    - OR Launching the **Mission Control app** from **Launchpad**.
- #### **Split View (Multi-App Usage)**
	1. Hover over an app’s **full-screen button** (Green button **top-left**).
	2. Choose:
	    - **Tile Window to Left of Screen**
	    - **Tile Window to Right of Screen**
	3. Select a second app for **side-by-side use**.



### **Key Takeaways**
- **Finder** is central to file navigation (**Go Pane, Shortcuts, Preview Pane**).
- **Spotlight** is the fastest way to find files & apps (`Command + Spacebar`).
- **Mission Control & Split View** improve multi-tasking.
- **Terminal commands** allow advanced navigation (`mv`, `defaults write`).



### Questions
- Download the above file and double click on it to unzip it. The extracted folder may appear empty, but in reality it has a hidden file with the flag. Can you find the flag?
	- HTB{F1l3s_c@n_Hide}
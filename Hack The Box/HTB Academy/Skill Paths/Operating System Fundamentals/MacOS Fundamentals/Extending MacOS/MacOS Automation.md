### Introduction
- Increase productivity by relying more on the keyboard and less on the mouse.
- Typing commands and using shortcuts is faster than manually moving the cursor.
- Learn shortcuts for quick folder navigation and application opening, e.g.,
    - Open a new `Finder` window with [`CMD+N`].
    - Navigate folders with arrow keys and [`CMD+↑`]/[`CMD+↓`].
- Use `Spotlight` search for efficiency:
    - Open it with [`CMD+SPACEBAR`] or the `F4` magnifying glass key.
    - Type the name of a file, folder, or app to open it instantly.
- This approach saves time and enables quick task starts in seconds.



### Alfred
- **Alfred App**: A powerful productivity tool for macOS that enhances efficiency with hotkeys, keywords, text expansion, and custom actions.
- **Advantages over macOS Spotlight**:
    - Instantaneous search results as you type.
    - Ability to traverse directories and perform actions directly in the search bar.
    - Customizable actions and support for applying actions to multiple results via a buffer.
- **Key Features**:
    - **Clipboard History**:
        - Access recent clipboard items with [`CMD+OPTION+C`].
        - Retains clipboard history for weeks and excludes sensitive items automatically.
        - **Clipboard Merging**: Combine multiple copied items into one using [`CMD+C+C`].
    - **Additional Tools**: Includes workflows, system commands, shell integration, text expansion, and quick look features.
- **Getting Started**:
    - Begin with simple features, like file search, and gradually explore advanced options.
    - The app is free, but advanced features require a one-time purchase.
- **Recommendation**: Alfred significantly boosts productivity and quickly becomes indispensable for frequent macOS users.



### Automation
- **Automate Repetitive Tasks**: Automating daily repetitive tasks saves significant time in the long run.
- **Alfred Workflows**: A powerful feature for macOS automation that enables performing specific actions directly from the search bar.
    - **Community Workflow Store**: Access open-source workflows for tasks like unit conversion (e.g., [Calculate Anything](https://github.com/biati-digital/alfred-calculate-anything)).
    - **Custom Workflows**: Create personalized workflows using Alfred's editor and scripting languages like Bash, Python, or PHP.
- **Example Use Case**: Automate creating a directory structure for pentests to execute the task with a single command.
- **Recommendation**: Start by exploring prebuilt workflows and progress to creating custom solutions to maximize productivity.



### Scripting
- Perhaps the most common way of automation is through scripting, which can be done through common scripting languages supported by macOS by default, like `Bash`, `Python`, or `JavaScript`. 
- MacOS even has its own `AppleScript` language, which should be more straightforward than some languages and allows easy access to more macOS features.
- Some specific advanced tasks require manual scripting, like backing up our operating system, running some development tests, or even deploying applications we may be developing. 
- These tasks tend to be repetitive with minor adjustments but usually take a long time to perform. 
- So, automating these tasks through scripting languages will save us a lot of time, be more productive, and make our lives much easier, even if writing the initial scripts may take several days.



### macOS Shortcuts
- Finally, we can utilize Apple's most recent automation tool [Shortcuts](https://support.apple.com/en-gb/guide/shortcuts-mac/apdf22b0444c/mac), which is built as a cross-platform automation tool to automate various tasks securely and can even be synced and run on other Apple devices, like iPhones or iPads with varying abilities.
- Shortcuts, just like Alfred Workflows, has an easy-to-use editor that allows us to select from various inputs, outputs, and actions to build our custom workflow.
- For example, we can choose the input to be the `last five photos in the Photos app`, select our action as `Make Gif`, and then select the output as `Send through Messages`. 
- This workflow takes less than a minute to set up and can be used on any of our Apple devices with a single click.
- Shortcuts can also be used to create advanced automation and can then be freely shared as an open-source shortcut. 
- We can even find stores for user-created shortcuts, like [ShortcutsGallery](https://shortcutsgallery.com) or [RoutineHub](https://routinehub.co), in which we may find many shortcuts we may find helpful. 
- The main advantage of using the shortcuts app (vs. Alfred Workflows or scripts) is the security aspect. 
- Apple requires user consent before running any sensitive action and only grants the shortcut action to any of your files after your approval. 
- Still, any publicly shared automation script may contain malicious content, so `always be very careful when selecting one` and read reviews on it before doing so.
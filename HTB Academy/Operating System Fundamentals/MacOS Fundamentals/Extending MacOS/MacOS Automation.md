- We can significantly increase our productivity on any operating system by relying more on the keyboard and using the mouse less. 
- This is because we can quickly type commands and shortcuts through our keyboard, while we need to manually move our cursor to a specific point on the screen multiple times if we rely on the mouse. 
- To utilize this, we can start by learning shortcuts to navigate folders quickly and open applications quickly. 
- For example, we can open a new `Finder` window by clicking [`CMD+N`], and then we can easily navigate to the folder we want by using the keyboard arrows and [`CMD+↑`]/[`CMD+↓`] to go in and out of folders.
- However, relying on the `Spotlight` search bar can still be much more efficient. 
- We can quickly bring up our search bar with the [`CMD+SPACEBAR`] shortcut or by clicking on the magnifying glass key on our keyboards 'usually on `F4`'. 
- Next, we can type the name of any file, folder, or application and select it from the results to open it. 
- Relying on this method, instead of manually finding each file/folder/application by manual mouse clicks, can save us hours of our life in the long run and will make us quickly start working on any task in a matter of 1-2 seconds.


### Alfred
- We can still be more efficient by utilizing one of the best productivity apps available for macOS, [Alfred](https://www.alfredapp.com). As mentioned on their website, "_Alfred is an award-winning app for macOS which boosts your efficiency with hotkeys, keywords, text expansion, and more. Search your Mac and the web, and be more productive with custom actions to control your Mac._". 
- To simplify it, Alfred is a more powerful macOS search bar, so let's discuss some of its powerful features.
- First, when comparing the built-in macOS search bar and Alfred, we will see that Alfred shows the search results instantaneously as we type, making it even `faster` to perform actions through the search bar. 
- In addition to that, it allows us to [traverse directories](https://www.alfredapp.com/help/features/file-search/) in the search results right within the search bar.
- We can also show the `Actions` to any search result by clicking the right key, which brings different possible actions based on the result type and even allows us to program custom actions. 
- We can even use a `buffer` to apply actions on multiple search results.
- One of the most powerful features in Alfred is its [clipboard history](https://www.alfredapp.com/help/features/clipboard/), which will become a feature you cannot work without once you start using it. 
- Once installed, Alfred will begin keeping a record of our recent clipboard, allowing us to access them at any time with the [`CMD+OPTION+C`] shortcut. 
- This provides ease of mind that we will not lose our current clipboard, so we can copy other things and then get back to an earlier clipboard result even weeks later!
- We can search through our clipboard history and remove specific instances if we find them to be sensitive, like passwords, even though Alfred will automatically exclude sensitive clipboard items from its history. 
- Another unique feature is `clipboard merging`, which allows us to copy multiple items to the same clipboard by clicking [`CMD+C+C`], so we can paste them as a single item (separated by a delimiter we configure).
- Alfred provides all of this and many more features, like `Workflows`, `system commands`, `shell integration`, `text expansion`, and `quick look`, all of which you can learn about on their [website](https://www.alfredapp.com). 
- This may sound overwhelming to understand initially, but we recommend you start with a single feature (like searching for files) and only start using a new one once you master the first. 
- This should quickly place a feature at your fingertips, and you will find yourself using it without knowing. 
- Alfred is free to use, but some of its main features are locked under a one-time purchase pack.

### Automation
- An important productivity rule states that we should always `automate repetitive tasks`.
- Whenever we find ourselves doing a specific task over and over every day, it is best to try to automate it, as it will save us a compounded amount of time in the long run. 
- For example, if we find ourselves creating a specific directory structure for every new pentest, then we can automate this task to create this directory with a single click. 
- While many of the basic actions can be automated through Alfred, as mentioned above, some more advanced steps will require programming, which we can accomplish with `workflows`.
- The most powerful feature of Alfred is its [workflows](https://www.alfredapp.com/workflows/), which perform specific actions through the search bar and is an ideal way for macOS automation. 
- Alfred provides a free store for all open-source workflows provided by the community, in which we can find many workflows that can automate many of the tasks we need or make it easier to perform other tasks.
- For example, we can use the [calculate anything](https://github.com/biati-digital/alfred-calculate-anything) workflow to convert units right within the search bar, like currency, time, data, and most of the metric units.
- Best of all, Alfred allows us to program our own workflows through its easy-to-use editor, and we can follow its [documentation](https://www.alfredapp.com/help/workflows/) for more info on how to do that and may even use scripting languages within it, like `Bash`, `Python`, or `PHP`. 
- Alfred workflows can be one of the easiest and best ways to automate repetitive tasks, like the custom directory creation we mentioned earlier.


### Scripting
- Perhaps the most common way of automation is through scripting, which can be done through common scripting languages supported by macOS by default, like `Bash`, `Python`, or `JavaScript`. 
- MacOS even has its own `AppleScript` language, which should be more straightforward than some languages and allows easy access to more macOS features.
- Some specific advanced tasks require manual scripting, like backing up our operating system, running some development tests, or even deploying applications we may be developing. 
- These tasks tend to be repetitive with minor adjustments but usually take a long time to perform. 
- So, automating these tasks through scripting languages will save us a lot of time, be more productive, and make our lives much easier, even if writing the initial scripts may take several days.


### macOS Shortcuts
- Finally, we can utilize Apple's most recent automation tool [Shortcuts](https://support.apple.com/en-gb/guide/shortcuts-mac/apdf22b0444c/mac), which is built as a cross-platform automation tool to automate various tasks securely and can even be synced and run on other Apple devices, like iPhones or iPads with varying abilities.
- Shortcuts, just like Alfred Workflows, has an easy-to-use editor that allows us to select from various inputs, outputs, and actions to build our custom workflow.
- For example, we can choose the input to be the `last five photos in the Photos app`, select our action as `Make Gif`, and then select the output as `Send through Messages`. This workflow takes less than a minute to set up and can be used on any of our Apple devices with a single click.
- Shortcuts can also be used to create advanced automation and can then be freely shared as an open-source shortcut. We can even find stores for user-created shortcuts, like [ShortcutsGallery](https://shortcutsgallery.com) or [RoutineHub](https://routinehub.co), in which we may find many shortcuts we may find helpful. 
- The main advantage of using the shortcuts app (vs. Alfred Workflows or scripts) is the security aspect. Apple requires user consent before running any sensitive action and only grants the shortcut action to any of your files after your approval. 
- Still, any publicly shared automation script may contain malicious content, so `always be very careful when selecting one` and read reviews on it before doing so.
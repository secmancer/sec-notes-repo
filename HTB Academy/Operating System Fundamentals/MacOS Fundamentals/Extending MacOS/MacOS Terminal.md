### macOS vs. Linux Terminals
- As we mentioned earlier, macOS and Linux are based on Unix design. While macOS is an officially certified UNIX operating system, Linux is UNIX-like, as it is based on Minix and not UNIX. 
- Minix was an attempt to copy the UNIX operating system without using any of their code (to avoid licensing), so we may find slight differences between the two operating systems. Most of the commands can still be used on both operating systems, as the UNIX shell is still at the core of both systems.
- Any [POSIX](https://en.wikipedia.org/wiki/POSIX) commands should work on both operating systems. If Bash scripts are denoted as [`#!/bin/sh`], then the script should be POSIX friendly and work on both macOS and Linux systems. 
- This is why we may find many penetration testing scripts written as POSIX scripts, like [nmapAutomator](https://github.com/21y4d/nmapAutomator) or [linPEAS](https://github.com/carlospolop/PEASS-ng/tree/master/linPEAS), as this makes them highly compatible with most UNIX systems (though making them a harder to code in Bash). 
- To find what commands are compatible with POSIX, you may check the POSIX tools (and the parameters and syntax they accept) in the [IEEE Std 1003.1-2017 Utilities specification](https://pubs.opengroup.org/onlinepubs/9699919799/idx/utilities.html), and the [IEEE Std 1003.1-2017 Built-ins specification](https://pubs.opengroup.org/onlinepubs/9699919799/idx/sbi.html).

> **Tip:** In a macOS terminal, you can use the `open` command to open any file with its default application. This can become handy when you want to open an image, a document, or even open a folder in Finder.


### ZSH
- In recent versions of macOS, Apple switched their default shell from `Bash` to `ZSH`, which is more versatile, user-friendly, and allows shell extensibility. ZSH is quite similar to Bash, but if you want to change the default shell to `bash` you can do so with the following command:
```
secmancer@htb[/htb]$ chsh -s /bin/bash
```
- If you are on an older version of macOS and would like to install ZSH, you can do so with the following command:
```
secmancer@htb[/htb]$ brew install zsh
secmancer@htb[/htb]$ chsh -s /bin/zsh
```
- While the main benefit of ZSH is its extensions, you may still find it more user-friendly than bash. 
- For example, whenever we click on `tab` after a command to show possible options/arguments, ZSH shows all of them below our command and allows us to navigate between them by clicking `tab`.
- Another example is traversing command history with the up arrow key. If we start writing a command (e.g., `cat /e`), clicking the up arrow would only show previous commands that begin with the command we wrote, making it easier to find the command we are looking for. 
- Such minor features make a big difference in your daily use of the shell, and once you get used to them, you will become more efficient in using your terminal.
- When we start a new terminal session, the default shell gets loaded with its default configuration. The default shell is ZSH, and its default configuration is stored at `~/.zshrc`. 
- A shell configuration file sets a few variables and executes a few commands to make your shell customized. For ZSH, we may also load some extensions or select our shell theme, as we will see later. 
- For beginners, you will usually only apply changes as instructed by extensions or plugins and will not need to make any custom changes.
- If you want to apply some default configurations, you can set up a few custom `aliases` that make it easier for you to use the shell. For example, I have the following `ls` aliases:
```
# Aliases
alias ll='ls -l'
alias la='ls -la'
alias l='ls -CF'
```
- This makes it easy for me to execute the frequently used `ls -la` command with `la`. 
- Similarly, I have an `archiving` function set up that allows me to easily extract any archive files through my terminal without needing to remember the different archive commands for each extension:
```
# Archives
function extract {
  if [ -z "$1" ]; then
    echo "Usage: extract <path/file_name>.<zip|rar|bz2|gz|tar|tbz2|tgz|Z|7z|xz|ex|tar.bz2|tar.gz|tar.xz>"
  else
    if [ -f $1 ]; then
      case $1 in
        *.tar.bz2)   tar xvjf $1    ;;
        *.tar.gz)    tar xvzf $1    ;;
        *.tar.xz)    tar xvJf $1    ;;
        *.lzma)      unlzma $1      ;;
        *.bz2)       bunzip2 $1     ;;
        *.rar)       unrar x -ad $1 ;;
        *.gz)        gunzip $1      ;;
        *.tar)       tar xvf $1     ;;
        *.tbz2)      tar xvjf $1    ;;
        *.tgz)       tar xvzf $1    ;;
        *.zip)       unzip $1       ;;
        *.Z)         uncompress $1  ;;
        *.7z)        7z x $1        ;;
        *.xz)        unxz $1        ;;
        *.exe)       cabextract $1  ;;
        *)           echo "extract: '$1' - unknown archive method" ;;
      esac
    else
      echo "$1 - file does not exist"
    fi
  fi
}
```
- Whenever I need to extract an archive, I can use the `extract FILENAME` command, which will use the matching command for that extension. This should give you an idea of what we may use the shell configuration file for.
 - As mentioned earlier, the main benefit of ZSH is the ability to install plugins and extensions to extend the default shell. One tool that makes it super easy to install and manage ZSH plugins and themes is [Oh My Zsh](https://ohmyz.sh), which we can install as follows:
```
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
- Most ZSH plugins have installation instructions, and most of them also provide instructions with/without `oh-my-zsh`, so you can choose whether you want to rely on it. Some plugins are only available through `oh-my-zsh`. 
- For example, let's try to install the `zsh-syntax-highlighting` plugin, which adds colors to our shell to denote incorrect commands and many other things. 
- To do so, we can first clone the plugin in the `custom/plugins` directory under oh-my-zsh, as mentioned in the plugin's installation instructions:
```
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```
- Now, all we need to do is to add the plugin's name inside the `plugins` variable in our ZSH configuration file:
```
plugins=(zsh-syntax-highlighting)
```
- Once we start a new terminal session, we should have colors in our shell.
- There are many other helpful ZSH plugins, like [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions) or [fzf](https://github.com/junegunn/fzf). Try to search for other plugins to find the ones you like.
- Finally, as seen in the earlier screenshots, we can set up a fantastic-looking terminal and shell. To do so, we will install the `powerlevel10k` ZSH plugin/theme through `oh-my-zsh`. We will also need to install a few fonts to enable icon usage within our terminal. 
- We will also install an HTB-exclusive macOS terminal configuration to have HTB colors in our terminal.
- Let's start by installing the necessary fonts, as mentioned by the `p10` [installation guide](https://github.com/romkatv/powerlevel10k#manual-font-installation). We can download these fonts and double-click them to install them:
	- [MesloLGS NF Regular.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Regular.ttf)
	- [MesloLGS NF Bold.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold.ttf)
	- [MesloLGS NF Italic.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Italic.ttf)
	- [MesloLGS NF Bold Italic.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold%20Italic.ttf) 

> **Note:** You would normally need to configure the terminal to use this font at this point. However, as we will be installing our own HTB terminal configurations, this will take care of that.

- Next, we can install the theme itself through `oh-my-zsh`, as follows:
```
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```
- Then we can add the following line in our ZSH configurations file `~/.zshrc`:
```
ZSH_THEME="powerlevel10k/powerlevel10k"
```

> **Note:** Once installed, the theme will ask you to configure it the next time you run the terminal, but you may close it and delay that until the end when we import our HTB profile.

- We may also install the theme through Homebrew, and it should take care of everything at once 'except for the fonts', as follows:
```
brew install romkatv/powerlevel10k/powerlevel10k
echo "source $(brew --prefix)/opt/powerlevel10k/powerlevel10k.zsh-theme" >>~/.zshrc
```
- With that, the theme should be installed, and the next time we run our terminal, it should take us through its initial setup to customize its look. 
- It will ask you some questions, and you should be able to answer `yes` to all and select the looks that suit your preferences.
- You may not like the default terminal ANSI colors, so you may configure your colors based on any terminal color palette you find online. 
- In this case, we will use our own Hack The Box terminal color palette. To install it, you can download the terminal configuration file from [this link](https://academy.hackthebox.com/storage/modules/157/htb_terminal.zip).
- Once you extract it, you can double-click it to install it. You may also install it through `Preferences`>`Profiles` and click on the `+` icon to import it.
- Finally, you should be able to see the `HTB` profile under the profiles menu, and you can click on it and then click on the `Default` button at the bottom to make it the default profile. `Now, you should have an awesome-looking terminal on your macOS system`.

> **Note:** The 'HTB.terminal' file may be blocked the first time you run it, for macOS-related security purposes. It is safe to run as it is created by us at Hack The Box. You can bypass the warning by going to 'System Preferences > Security and Privacy > General' and selecting 'open anyway'.


### Questions
- Read the zsh configuration shown in the section above to find what command is mapped to 'll'. Submit the command as the answer.
	- ls -l
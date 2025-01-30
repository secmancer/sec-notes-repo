## **1. macOS vs. Linux Terminals**
- 💡 **macOS is a certified UNIX operating system, while Linux is UNIX-like.**
- #### **Key Differences & Similarities:**
	- **POSIX compatibility:** Most standard POSIX commands work on both systems.
	- **Default shell:**
	    - **macOS:** **ZSH** (since macOS Catalina, 10.15).
	    - **Linux:** Typically **Bash** (default on most distributions).
	- **Open command:**
	    - macOS provides the `open` command to launch files with default apps (`open file.pdf`).



## **2. Switching Between ZSH and Bash**
- **Change default shell to Bash:**
    ```bash
    chsh -s /bin/bash
    ```
- **Change default shell to ZSH (if using an older macOS version):**    
    ```bash
    brew install zsh
    chsh -s /bin/zsh
    ```
- 📌 **Why ZSH?**  
	- ✅ **Enhanced auto-completion** (navigable tab suggestions).  
	- ✅ **Improved command history search** (filters based on input).  
	- ✅ **Plugin support** (e.g., syntax highlighting, autosuggestions).



## **3. Configuring ZSH (`.zshrc` File)**
- 📌 **Location:** `~/.zshrc`
	- Stores user-specific shell preferences, aliases, and plugins.
- #### **Example: Custom Aliases for `ls`**
```bash
# Aliases
alias ll='ls -l'
alias la='ls -la'
alias l='ls -CF'
```
- #### **Example: Archive Extraction Function**
```bash
# Function to extract different archive formats
function extract {
  if [ -f "$1" ]; then
    case $1 in
      *.tar.bz2) tar xvjf "$1" ;;
      *.tar.gz) tar xvzf "$1" ;;
      *.tar.xz) tar xvJf "$1" ;;
      *.zip) unzip "$1" ;;
      *.rar) unrar x "$1" ;;
      *.7z) 7z x "$1" ;;
      *) echo "Unknown archive format" ;;
    esac
  else
    echo "File does not exist"
  fi
}
```
- ✅ **Usage:**
```bash
extract archive.tar.gz
```



## **4. Installing & Using ZSH Plugins**
- 📌 **Install Oh My Zsh (Plugin & Theme Manager)**
```bash
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
- 📌 **Example: Install Syntax Highlighting Plugin**
```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git \
${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```
- 📌 **Enable it in `~/.zshrc`:**
```bash
plugins=(zsh-syntax-highlighting)
```
- ✅ **Effect:** Highlights invalid commands and syntax errors in real time.
- 📌 **Other Useful Plugins:**
	- **`zsh-autosuggestions`** → Suggests commands based on history.
	- **`fzf`** → Fuzzy finder for command-line navigation.



## **5. Setting Up an Awesome Terminal**
- 📌 **Install Powerlevel10k Theme (P10K)**
```bash
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git \
${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```
- 📌 **Enable it in `~/.zshrc`:**
```bash
ZSH_THEME="powerlevel10k/powerlevel10k"
```
- ✅ **Effect:** Provides a highly customizable and modern terminal UI.
- 📌 **Alternative Installation via Homebrew:**
```bash
brew install romkatv/powerlevel10k/powerlevel10k
echo "source $(brew --prefix)/opt/powerlevel10k/powerlevel10k.zsh-theme" >>~/.zshrc
```



## **6. Customizing Terminal Fonts & Colors**
- 📌 **Install Nerd Fonts for Icons**
	1. Download and install:
	    - [MesloLGS NF Regular.ttf](https://github.com/ryanoasis/nerd-fonts/blob/master/patched-fonts/Meslo/L/Regular/MesloLGS%20NF%20Regular.ttf)
	    - [MesloLGS NF Bold.ttf](https://github.com/ryanoasis/nerd-fonts/blob/master/patched-fonts/Meslo/L/Bold/MesloLGS%20NF%20Bold.ttf)
	    - [MesloLGS NF Italic.ttf](https://github.com/ryanoasis/nerd-fonts/blob/master/patched-fonts/Meslo/L/Italic/MesloLGS%20NF%20Italic.ttf)
	    - [MesloLGS NF Bold Italic.ttf](https://github.com/ryanoasis/nerd-fonts/blob/master/patched-fonts/Meslo/L/Bold-Italic/MesloLGS%20NF%20Bold%20Italic.ttf)
- 📌 **Apply the Font in Terminal:**
	- `Preferences > Profiles > Text > Change Font > Select "MesloLGS NF"`
- 📌 **HTB Terminal Theme (Hack The Box Color Scheme)**
	- **Download the theme file** → [HTB.terminal](https://github.com/yourlink/HTB.terminal)
	- **Apply it:**
	    - **Double-click the file** or
	    - `Preferences > Profiles > Import > Select "HTB.terminal"`
- ✅ **Final Result:** A **beautiful, high-performance** terminal setup! 🎨💻



## **Summary**
🔹 **macOS terminal is UNIX-certified; similar to Linux but with unique features.**  
🔹 **ZSH (default shell) offers auto-completion, syntax highlighting & plugins.**  
🔹 **Customize `.zshrc` for aliases, shortcuts, and plugins.**  
🔹 **Install Oh My Zsh + Powerlevel10k for a modern terminal experience.**  
🔹 **Use Nerd Fonts & custom themes to enhance visuals.**



### Questions
- Read the zsh configuration shown in the section above to find what command is mapped to 'll'. Submit the command as the answer.
	- ls -l
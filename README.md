# WSL OH MY ZSH
## Install WSL 2
Follow [Install wsl 2](https://docs.microsoft.com/en-us/windows/wsl/install-win10) from microsoft blog
## Install ZSH && Oh-my-zsh
```bash
# Install zsh
sudo apt-get install zsh
# Install  oh-my zsh
curl -Lo install.sh https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh
sh install.sh
# Set zsh as default terminal
chsh -s /usr/bin/zsh
```
## Install [zsh-nvm](https://github.com/lukechilds/zsh-nvm)

```bash
# Clone this repository somewhere (~/.zsh-nvm for example)
git clone https://github.com/lukechilds/zsh-nvm.git ~/.zsh-nvm
# Source it in your .zshrc (or .bashrc)
source ~/.zsh-nvm/zsh-nvm.plugin.zsh
# Upgrade to the latest release of nvm
nvm upgrade
```
## Install Node.js
You can install the latest Node.js nightlies or release candidates with nvm install nightly|rc. Aliases will automatically be created so you can easily nvm use nightly|rc in the future:
```bash
nvm install rc
# Update npm
npm install -g npm@7.20.5
```
Add nvm to zshrc, It must be set before zsh-nvm is loaded.
```bash
nano ~/.zshrc
# Add before zsh-nvm is loaded
export NVM_DIR="$HOME/.nvm"
 [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"
```
## Install fonts
Install a powerlinefont from [nerdfonts.com](https://www.nerdfonts.com/font-downloads)
```bash
# Settings.json vs code example
"terminal.integrated.fontFamily": "JetBrainsMono Nerd Font Mono",
"terminal.integrated.fontWeightBold": "500",
```
# Bonus: Agnoster Theme Configs
###  Hide username & machine name from prompt (Agnoster Theme)
Open your .zshrc and paste this at the bottom:
```bash
prompt_context() {
  if [[ "$USER" != "$DEFAULT_USER" || -n "$SSH_CLIENT" ]]; then
    prompt_segment black default "%(!.%{%F{yellow}%}.)$USER"
  fi
}
```
This makes only your username to appear. If you don't want that too, just comment out this line prompt_segment black default "%(!.%{%F{yellow}%}.)$USER"
### How to shorten zsh prompt 
```bash
# Step 1: check where oh-my-zsh installation is in ~/.zshrc
# Path to your oh-my-zsh installation.
export ZSH="/Users/shandou/.oh-my-zsh"
# Step 2: go to the installation directory and locate the themes sub-directory
cd /Users/shandou/.oh-my-zsh/themes/
# Step 3: edit the following line the theme you are using. Save the file and source ~/.zshrc
# Dir: current working directory
prompt_dir() {
  #prompt_segment blue $CURRENT_FG '%~'
  prompt_segment blue $CURRENT_FG '%2~'
}
```
Once you save the change and reload your setting via source ~/.zshrc, you should be able to see your shorter prompt taking effects ✨ ✨ 
## A workaround to you have unstaged changeserror when you need to update oh-my-zsh 
One quirk of oh-my-zsh installation is that it lives as a git repo in our system, and any subsequent upgrades we shall enjoy now become pulling new changes from the “mother” repo. Since we now have applied changes to shorten the prompt, directly pulling new changes would not be allowed unless we stash the changes. Luckily we only need the following command:
```bash
# Step 1: go to oh-my-zsh installation folder and stash the change you have made to the theme
$ cd ~/.oh-my-zsh && git stash
# Step 2: use this command to upgrade
$ upgrade_oh_my_zsh
# Step 3: after upgrade, re-apply your changes that are needed to shorten the prompt
$ git stash pop
```


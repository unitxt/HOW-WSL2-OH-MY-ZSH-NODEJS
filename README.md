# HOW WSL2 && OH MY ZSH + NODEJS
### Install WSL2
How [Install wsl2](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
### Install ZSH && Oh-my-zsh
```bash
# Install zsh
sudo apt-get install zsh
# Install  oh-my zsh
curl -Lo install.sh https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh
sh install.sh
# Set zsh as default terminal
chsh -s /usr/bin/zsh
```
### Install [zsh-nvm](https://github.com/lukechilds/zsh-nvm)

```bash
# Clone this repository somewhere (~/.zsh-nvm for example)
git clone https://github.com/lukechilds/zsh-nvm.git ~/.zsh-nvm
# Source it in your .zshrc (or .bashrc)
source ~/.zsh-nvm/zsh-nvm.plugin.zsh
# Upgrade to the latest release of nvm
nvm upgrade
```
### Install Node.js
You can install the latest Node.js nightlies or release candidates with nvm install nightly|rc. Aliases will automatically be created so you can easily nvm use nightly|rc in the future:
```bash
# Example: nvm install 14.17.5
nvm install <version>
```
Add nvm env var to zshrc, It must be set before zsh-nvm is loaded `nano ~/.zshrc`
```bash
# Add before zsh-nvm is loaded
export NVM_DIR="$HOME/.nvm"
 [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"
```
### Install fonts
Install a powerlinefont in windows from [nerdfonts.com](https://www.nerdfonts.com/font-downloads)
```bash
# Settings.json vs code example
"terminal.integrated.fontFamily": "JetBrainsMono Nerd Font Mono",
"terminal.integrated.fontWeightBold": "500",
```
### Install Theme

Visit [powerlevel10k](https://github.com/romkatv/powerlevel10k), add theme to oh-my-zsh `nano ~/.zshrc`:

```bash
ZSH_THEME="powerlevel10k/powerlevel10k"
```
 
 ### Remove ZSH Underline
```bash
 (( ${+ZSH_HIGHLIGHT_STYLES} )) || typeset -A ZSH_HIGHLIGHT_STYLES
ZSH_HIGHLIGHT_STYLES[path]=none
ZSH_HIGHLIGHT_STYLES[path_prefix]=none
```
### WSL2 config for Windows Terminal

To fix it you need to modify the settings.json file of Windows Terminal (which you can open with keyboard shotrcut: Ctrl + ,).

Once in the settings json file find the WSL entry and set the startingDirectory to the network path of your WSL home directory:

```json
{
    "guid": "{c6eaf9f4-32a7-5fdc-b5cf-066e43243e40}",
    "hidden": false,
    "name": "Ubuntu",
    "source": "Windows.Terminal.Wsl",
    "startingDirectory": "//wsl$/Ubuntu/home/<user>/"
},
```
### Remove Bash Dir Background

Copy and paste at bottom of ~/.bashrc and source it, [stackoverflow](https://stackoverflow.com/questions/40574819/how-to-remove-dir-background-in-ls-color-output)

```bash
eval "$(dircolors -p | \
    sed 's/ 4[0-9];/ 01;/; s/;4[0-9];/;01;/g; s/;4[0-9] /;01 /' | \
    dircolors /dev/stdin)"
```

# Zsh on Ububtu Subsystem Windows 10

Instrucciones de Instalación

### Instalar ZSH 

Para instalar ZSH, en la terminal ejecutamos el siguiente comando:

```bash
sudo apt-get install zsh
```

Nos pedirá la contraseña del superusuario, la escribimos y después tendremos que escribir Y para confirmar que queremos instalar ese paquete

### Instalar Oh-my-zsh

En la terminal ingresamos los siguientes comandos:

```bash
curl -Lo install.sh https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh
sh install.sh
```

A la mitad del proceso nos preguntará si deseamos que zsh sea nuestra terminal por defecto y escribiremos Y para aceptar e ingresamos nuestra contraseña de superusuario para que pueda continuar.

### Definir ZSH como terminal por defecto

Ejecutaremos el siguiente comando en la terminal e inmediatamente nos pedirá la contraseña de superusuario:

```bash
chsh -s /usr/bin/zsh
```
### WSL 1

Solo en WSL1: Muchas veces eso no es suficiente, por lo que le tenemos que indicar al archivo de configuración (.bashrc) la terminal que debe de ejecutar y para eso, realizamos los siguientes pasos:

Ejecutamos el siguiente comando: nano ~/.bashrc
En la parte superior del archivo agregamos las siguientes líneas:

```bash
if test -t 1; then
exec zsh
fi
```

Esto con el fin de ejecutar siempre zsh como terminal por defecto y no tenga problemas con otras aplicaciones del sistema (porque es Windows lol)

Para terminar, presionamos Ctrl + X y después Y para aceptar los cambios
Para confirmar estos cambios en el archivo ejecutamos cat ~/.bashrc y corroboramos que estén las líneas que agregamos.

### WSL 1 && WSL 2

Por último, volvemos a ejecutar el siguiente comando:

```bash
chsh -s /usr/bin/zsh
```

### Install zsh-nvm 💥💥

Clone this repository somewhere (~/.zsh-nvm for example)

```bash
git clone https://github.com/lukechilds/zsh-nvm.git ~/.zsh-nvm
```
Then source it in your .zshrc (or .bashrc)

```bash
source ~/.zsh-nvm/zsh-nvm.plugin.zsh
```

Upgrade to the latest release of nvm:

```bash
source ~/.zsh-nvm/zsh-nvm.plugin.zsh
```
### Install node 💥💥

You can install the latest Node.js nightlies or release candidates with nvm install nightly|rc. Aliases will automatically be created so you can easily nvm use nightly|rc in the future:

```bash
nvm install rc
```
Update npm

```bash
npm install -g npm@7.20.5
```

Add nvm to zshrc, It must be set before zsh-nvm is loaded.

```bash

nano ~/.zshrc

# add this before zsh-nvm is loaded

export NVM_DIR="$HOME/.nvm"
 [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"

```

## WSL1 1 Config 

### Config zsh-nvm 💥💥

```bash

nano ~/.zshrc

# Add in your ~/.zshrc the following:

plugins+=(zsh-nvm)

export NVM_DIR="$HOME/.nvm"
 [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"

source ~/.zshrc

# Usage :

nvm install node

  ```

## Install font ❤️❤️

Instal firecode or download another from nerdfonts.com

```bash
git clone https://github.com/tonsky/FiraCode.git
```

Edit settings.json Vs Code

```bash
"terminal.integrated.fontFamily": "Fira Code",
"terminal.integrated.fontWeightBold": "900",
```

## Agnoster Theme Config

###  Hide username & machine name from prompt (Agnoster Theme)🔥🔥
 
Open your .zshrc and paste this at the bottom:

```bash
prompt_context() {
  if [[ "$USER" != "$DEFAULT_USER" || -n "$SSH_CLIENT" ]]; then
    prompt_segment black default "%(!.%{%F{yellow}%}.)$USER"
  fi
}
```

This makes only your username to appear. If you don't want that too, just comment out this line prompt_segment black default "%(!.%{%F{yellow}%}.)$USER"

### How to shorten zsh prompt ✂️✂️

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

## A workaround to you have unstaged changeserror when you need to update oh-my-zsh 💩💩

One quirk of oh-my-zsh installation is that it lives as a git repo in our system, and any subsequent upgrades we shall enjoy now become pulling new changes from the “mother” repo. Since we now have applied changes to shorten the prompt, directly pulling new changes would not be allowed unless we stash the changes. Luckily we only need the following command:

```bash
# Step 1: go to oh-my-zsh installation folder and stash the change you have made to the theme
$ cd ~/.oh-my-zsh && git stash
# Step 2: use this command to upgrade
$ upgrade_oh_my_zsh
# Step 3: after upgrade, re-apply your changes that are needed to shorten the prompt
$ git stash pop
```
##  SSH Keys on  Ubuntu

```bash
ssh-keygen
```



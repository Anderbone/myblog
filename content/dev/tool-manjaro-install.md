+++ 
date = "2022-05-31"
title = "Manjaro new installation personal config"
tags = ["tool","linux"]
+++

Configure trackball: https://yanjiyu.com/dev/tool-deftpro/

system
```
sudo pacman-mirrors -f && sudo pacman -Syyu
sudo pacman -Syu base-devel --needed
sudo pacman -S yay go texlive-most konversation docker docker-compose gvim
sudo systemctl enable --now fstrim.timer
```

personal software
```
yay -S visual-studio-code-bin
yay -S dynalist
yay -S stretchly
yay -S todoist-appimage
yay -S jetbrains-toolbox 
yay -S autokey-git
yay -S flameshot
yay -S eudic
yay -S freedownloadmanager
yay -S git-review
python3 -m pip install --upgrade 'maestral[gui]'
pip install --user tldr
```

git
```
git config --global user.email "yanchiyu@outlook.com" 
git config --global user.name "Anderbone"
```
oh my zsh
```
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```
.zshrc
```
# If you come from bash you might have to change your $PATH.
# export PATH=$HOME/bin:/usr/local/bin:$PATH

# Path to your oh-my-zsh installation.
export ZSH="$HOME/.oh-my-zsh"

# Set name of the theme to load --- if set to "random", it will
# load a random theme each time oh-my-zsh is loaded, in which case,
# to know which specific one was loaded, run: echo $RANDOM_THEME
# See https://github.com/ohmyzsh/ohmyzsh/wiki/Themes
ZSH_THEME="robbyrussell"

# Uncomment one of the following lines to change the auto-update behavior
zstyle ':omz:update' mode disabled  # disable automatic updates
# zstyle ':omz:update' mode auto      # update automatically without asking
# zstyle ':omz:update' mode reminder  # just remind me to update when it's time

# Uncomment the following line to change how often to auto-update (in days).
# zstyle ':omz:update' frequency 13


# Uncomment the following line if you want to disable marking untracked files
# under VCS as dirty. This makes repository status check for large repositories
# much, much faster.
DISABLE_UNTRACKED_FILES_DIRTY="true"

# Uncomment the following line if you want to change the command execution time
# stamp shown in the history command output.
# You can set one of the optional three formats:
# "mm/dd/yyyy"|"dd.mm.yyyy"|"yyyy-mm-dd"
# or set a custom format using the strftime function format specifications,
# see 'man strftime' for details.
# HIST_STAMPS="mm/dd/yyyy"

# Would you like to use another custom folder than $ZSH/custom?
# ZSH_CUSTOM=/path/to/new-custom-folder

plugins=(
	git
	archlinux
	docker
	docker-compose
	npm
	sudo
	vscode
	web-search
	history-substring-search
	zsh-autosuggestions
	zsh-syntax-highlighting
)

source $ZSH/oh-my-zsh.sh

# User configuration

# export MANPATH="/usr/local/man:$MANPATH"

# You may need to manually set your language environment
# export LANG=en_US.UTF-8

# Preferred editor for local and remote sessions
# if [[ -n $SSH_CONNECTION ]]; then
#   export EDITOR='vim'
# else
#   export EDITOR='mvim'
# fi

# Compilation flags
# export ARCHFLAGS="-arch x86_64"

# Set personal aliases, overriding those provided by oh-my-zsh libs,
# plugins, and themes. Aliases can be placed here, though oh-my-zsh
# users are encouraged to define aliases within the ZSH_CUSTOM folder.
# For a full list of active aliases, run `alias`.
#
# Example aliases
# alias zshconfig="mate ~/.zshrc"
# alias ohmyzsh="mate ~/.oh-my-zsh"

# Key mapping
bindkey '^H' backward-kill-word

alias eudic='/home/jiyu/Applications/eudic_3607f62f9b8228131f9f4b0f97be4cbf.AppImage %F'
```

mount drive, check UUID, then edit /etc/fstab and insert one line.
```
lsblk -f
UUID=xxx  /mypath ext4 defaults 0 0
```
Chinese input
```
open Manjaro Hello, Extended language support
tick 'Manjaro Asian Input Support Fcitx', then click 'Update System'
```

kde widgets
```
speed, config, choose only text
```
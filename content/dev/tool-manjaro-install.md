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

Final version:

![](https://i.imgur.com/uYxWTHh.jpg)
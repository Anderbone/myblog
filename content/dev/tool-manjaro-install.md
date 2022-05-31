+++ 
date = "2022-05-31"
title = "Manjaro new installation personal config"
tags = ["tool","linux"]
+++

Configure trackball: https://yanjiyu.com/dev/tool-deftpro/

system
```
sudo pacman-mirrors -f && sudo pacman -Syyu
sudo pacman -S yay vim
```

personal software
```
yay -S visual-studio-code-bin
yay -S microsoft-edge-stable
yay -S dynalist
yay -S jetbrains-toolbox 
python3 -m pip install --upgrade 'maestral[gui]'
```

git
```
git config --global user.email "yanchiyu@outlook.com" 
git config --global user.name "Anderbone"
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
+++ 
date = "2020-05-17"
title = "Install VMware Workstation on Manjaro"
tags = ["tool", "manjaro", "vmware" ]
+++

## vmmon error
After installation, you can't open VMware directly. It will show an error:
> VMWare could not find module ‘vmmon’, Please Make Sure That The Kernel Module 'vmmon' Is Loaded.

[manjaro wiki](https://wiki.manjaro.org/index.php?title=VMware#Installing_VMWare_Workstation_on_Manjaro)

The AUR package vmware-workstation will install VMWare Workstation and the dkms modules needed to run it.

It can be installed with:
```
 pamac build vmware-workstation
```
After installing, either reboot, or load the required modules
```
 sudo modprobe -a vmw_vmci vmmon
```

There are three services that can be optionally be enabled:
```
vmware-networks.service: Provides network access inside VMs, most people will want this enabled
vmware-usbarbitrator.service: Allows USB devices to be connected inside VMs
vmware-hostd.service: Enables sharing of VMs on the network
```
To start and enable these services use:
```
 sudo systemctl enable --now vmware-networks.service
 sudo systemctl enable --now vmware-usbarbitrator.service
 sudo systemctl enable --now vmware-hostd.service
```

## floppy drive

The first time I accidently installed it on floppy drive, the default choice should be a CD drive.
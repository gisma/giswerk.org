---
layout: default
title: Setup Nvidia GPUs for Agisoft
parent: agisoft
nav_order: 2
---
# Setup Nvidia GPUs for Agisoft

After a long run finally here is one successful solution for setting up consumer GPUs from Nvidia for a use with Agisoft. A lot of it is compiled on [abhay's](http://abhay.harpale.net/blog/linux/nvidia-gtx-1080-installation-on-ubuntu-16-04-lts/) blog.

The following solution worked for a workstation server with Titan-X devices:

	:::bash
	# not sure if necessary but finally sucessful
	sudo apt-get install mesa-common-dev-lts-xenial 
	sudo apt-get install mesa-common-dev
	sudo apt-get install mesa-common
	sudo apt-get install libssl1.0.0
	sudo apt-get install libtxc-dxtn-s2tc-bin
	sudo apt-get install --reinstall xserver-xorg-video-intel libgl1-mesa-glx libgl1-mesa-dri xserver-xorg-core 
	sudo apt-get install freeglut3-dev


	:::bash
	sudo nano  /etc/modprobe.d/blacklist.conf
	blacklist amd76x_edac
	blacklist vga16gb
	blacklist nouveau
	blacklist rivafb
	blacklist nvidiafb
	blacklist rivatv
	
	# open a bash terminal as root
	sudo bash
	# remove existing nvidia stuff
	apt-get purge nvidia-*
	apt autoremove 
	# 1st reboot
	shutdown -r now
	
	# remove remains of nvidia stuff
	# login as root
	sudo bash
	apt-get remove --purge nvidia*
	dpkg --configure -a
	
	# 2nd reboot
	shutdown -r now
	
	# login as root
	sudo bash
	# if so stop the GUI
	service lightdm stop 
	# stop the X-server if so
	killall xinit 
	# download the latest nvidia drivers. for titan-x currently NVIDIA-Linux-x86_64-367.44.run was the latest
	cd ~/Downloads/
	wget us.download.nvidia.com/XFree86/Linux-x86_64/367.35/NVIDIA-Linux-x86_64-367.35.run 
	# make the downloaded file an executable and run  the NVidia installer
	chmod +x NVIDIA-Linux-x86_64-367.35.run
	./NVIDIA-Linux-x86_64-367.35.run 
	
	# follow the prompts in the process
	# once the process is over, reboot
	shutdown -r now
	


Done


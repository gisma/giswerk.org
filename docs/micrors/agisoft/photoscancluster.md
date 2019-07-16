---
layout: default
title: Setup Photoscan on a cluster
parent: Agisoft Photoscan
grand_parent: Micro Remote Sensing
nav_order: 1
---
# Setup Photoscan on a cluster

The concept is roughly outlined in chapter 8 of the Agisoft Photoscan [ manual](http://www.agisoft.com/pdf/photoscan-pro_1_3_en.pdf). Nevertheless there atre some pitfalls and not so well documented features.

First you need to export a common net ressource. You may follow the [[https://www.digitalocean.com/community/tutorials/how-to-set-up-an-nfs-mount-on-ubuntu-16-04
 | digitialocean]] example:
 | ------------------------

	:::bash
	# on the sever side (exporting machine)
	sudo apt-get install nfs-kernel-server
	sudo mkdir /var/nfs/general -p
	sudo chown nobody:nogroup /var/nfs/general
	sudo nano /etc/exports
	/var/nfs/general    xxx.xxx.xxx.xxx(rw,sync,no_subtree_check)
	sudo systemctl restart nfs-kernel-server
	
	# on the clients side
	sudo apt-get install nfs-common
	sudo mkdir /var/nfs/agi -p
	sudo mount xxx.xxx.xxx.xxx:/var/nfs/general /var/nfs/agi
	


Now you have to start a head node as photoscan server

	:::bash
	
	nohup ./photoscan.sh --server xxx.xxx.xxx.xxx --dispatch xxx.xxx.xxx.xxx  --root /var/nfs/agi


Next you may assign node(s)

	:::bash
	
	nohup ./photoscan.sh --node --dispatch xxx.xxx.xxx.xxx  --opencl_gpu_mask 1  --root /var/nfs/agi



`<note>`
Be aware, that the monitor and the network installation of Agisoft Photoscan **must** have the same version.
The installation on the computer can have a newer version.
`</note>`

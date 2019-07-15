---
layout: default
title: Customization
nav_order: 4
---
# uavR packages 

## Supported UAV platforms

The reason using DJI is their absolute straightforward usage. Everybody can fly with a DJI but the price to pay off is a hermetically closed system. Only the litchi app provides additionally to a cloud based mission planer an offline/standalone interface that is up to date and facilitate the upload of a CSV formatted waypoint file to control autonomous flights with the the Phantom.

The open uav community is focused on the PixHawk autopilot unit and the Mission Planner software. It is well documented and several APIs are provided. Nevertheless an affordable terrain following autonomous flight planning tool is not available yet. ''makeFP'' creates  MAV format compliant mission files that are ready to upload to the Pixhawk controller using the ''upload2Solo'' function.

## The uavR Family

The package family consists of 4 parts:


*  flight planning ''uavRmp''

*  remote sensing ''uavRrst''

    

Up to now it has been dedicated to low budget rtf-UAVs as the DJI Phantom series and the 3DR Solo. However the current and future support will cover all Pixhawk based UAVs.



## uavRmp

The open UAV community is focused on the PixHawk autopilot unit and the ''[MissionPlanner](http://ardupilot.org/planner/)'' or ''[APM Planner 2](http://ardupilot.org/planner2/)'' software. Both are well documented and provide APIs and easy to use GUIs. Nevertheless they are missing planning capability (APM Planner) or an terrain following autonomous flight planning tool, that is also dealing with battery-dependent task splitting and save departures and approaches (MissionPlanner) yet. Other commercial competitors like the powerful ''[ugcs](https///www.ugcs.com/)'' software package are still lacking an advanced feature for generating smooth and save  surface following flights for low AGL flights.

The ''uavRmd'' package bridges this gap  and generates ''MAVLINK'' format compliant mission files that can be uploaded to the Pixhawk controller using an integrated function or externally by any Ground Control Station software.

The reason using DJI platforms is their absolute straightforward usage. Everybody can fly with a DJI but the price to pay off is a hermetically closed system. Only the litchi app provides additionally to a cloud based mission planer an offline/standalone interface that is up to date and facilitate the upload of a CSV formatted waypoint file to control autonomous flights with the the Phantom.


The ''[ uavRmp](https///cran.r-project.org/web/packages/uavRmp/index.html)'' package is hosted on CRAN  and designed for UAV autonomous mission planning. In the first place it is a simple and open source planning tool for monitoring flights of low budget drones based on ''R''. It provide an easy workflow for planning autonomous surveys including battery-dependent task splitting and save departures and approaches of each monitoring chunks. It belongs to the ```uavR``` package family that provides more functionality for the pre- and post-processing as well as the analysis of the derived data.


The core planning function ''makeFP'' (make flight plan) generates either intermediate flight control files for the DJI Phantom x UAVs or ready to upload control files for the Pixhawk/3DR Solo. The DJI control files are designed for using with the proprietary ''[Litchi](https///flylitchi.com/)'' flight control app exchange format, while the 3DR Solo files are using the ''MAVLINK'' common message format, that is used by the PixHawk flight controller family.

Please note that you will find on github the latest  ''[ uavRmp](https///github.com/gisma/uavRmp)'' release. 


## uavRst


The sister package ''[ uavRst](https///github.com/gisma/uavRst)'' is not hosted on CRAN yet. It  makes heavy use of GRASS7, SAGA GIS, JS, Python OTB and some other CLI tools. The setup of the correct linkage to these APIs can be cumbersome. For using the uavRST package you need to install the ''[ link2GI](https///cran.r-project.org/web/packages/link2GI/index.html)'' package. 

Nevertheless all mentioned software packages have to be installed correctly on your the OS. It is just in parts tested under Windows but should run....The most easiest way to obtain a fairly good run time environment is to setup Linux as a dual boot system or in a VB. If interested in setting up a clean Xubuntu or Mint Linux and then use the post install script for installing most of the stuff. For using some of the the Solo related functions you need to install the dronekit python libs in addition.

A full list of necessary libraries and binaries beyond R will soon be provided.

Even if honestly working on it it will be still a long run passing the CRAN check, nevertheless it runs fine for now ...

## Installation uavRmp



	:::rsplus
	# current CRAN version of the missionplanner
	install.packages("uavRmp")
	
	# latest github version
	devtools::install_github("gisma/uavRmp", ref = "master")


If you want to install all dependencies use:

	:::rsplus
	devtools::install_github("gisma/uavRmp", ref = "master", dependencies = TRUE)


## Installation uavRmp



	:::rsplus
	
	# latest github version
	devtools::install_github("gisma/uavRst", ref = "master")


If you want to install all dependencies use:

	:::rsplus
	devtools::install_github("gisma/uavRst", ref = "master", dependencies = TRUE)



`<note important>`The package development is a work in progress and you will find more information on [uavR gitbub](https///github.com/gisma) pages. `</note>`

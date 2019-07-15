---
layout: default
title: Customization
nav_order: 4
---
# DJI Flight Planning Tutorial

## Introduction

The flightplanning cookbook is addressing the utilisation of ready to fly (rtf) unmanned aerial vehicles (uav) for remote sensing purposes. The basic idea is to use rtf-uavs for advanced high resolution data retrievals. The range is widespread from Digital Surface Models (DSM), Digital Elevation Models (DEM), orthophotos, altitude point clouds to landuse/landscape classification, NDVI forest structure classifications and so on… 

This document will cover in brief the recipe to solve the all day problems of typical survey planning. A deeper discussion and knowledge base is provided at the [micro remote sensing ](http://giswerk.org/doku.php?id=projekte:micrors:intro) (mRS) wiki.

## Overview of the task


This recipe deals with the effective and safe planning of an autonomous flight. This covers necessary hardware and software as well as supplemental data and nice to haves.
## Skills you will learn


In the extended version you find some more explanations and hints for improving your planning. Even if you can assume the use of  uavs for Remote Sensing (RS) purposes as “operational” you should always keep in mind that avoiding negative impacts is a result of ￼responsible and focused planning.

`<note warning>`Please keep in mind that autonomous uavs are dangerous for the environment as well as you easily can loss or damage them. 
`</note>`
## Things you need


 1.  [R](https///www.r-project.org/) (examples are in [RStudio](https///www.rstudio.com/))
 2.  [Robubu ](https///github.com/gisma/robubu)package
 3.  Digital Elevation Model data (depending on the area
 4.  DJI [Phantom 3](http://www.dji.com/product/phantom-3-pro) (P3) Advanced/Professional
 5.  [Litchi](https///flylitchi.com/) Flight App / [Tower App ](https///play.google.com/store/apps/details?id=org.droidplanner.android)
 6.  Time to work it out


## The Whys


### Why R


Easy to use and well known in the environmental research community. R is pretty flexible and there exist a lot of post processing and classification algorithm to head on after the flight planning. It seems to be (beside Python) the best approach to reach the people interested in mRS and to keep out the drone dudes ;-). 

### Why Phantom?


4k camera, easy to fly, cheap, fast, robust and fairly reliable to control.

### Why Litchi?


The main problem with DJI-stuff is that these guys control **everything **via their cloud which is obligate to use. Besides this kind of  “political” impacts there does not exist an interface for pushing waypoint data for autonomous flights to the P3 without using their cloud. The third party software Litchi provides an interface to the DJI uav family implemented as a webtool for conversion and upload of user generated csv/kml control files to the P3. 

## Flight planning

 

The planning of survey flights is depending on some constraints that will be discussed elsewhere. However for now some bullet points should be mentioned:

 1.  weather
 2.  topography
 3.  usage/protection state of the area
 4.  unknown physical obstacles (UPOs)
 5.  technical restrictions of the uav-platform
 6.  safety issues (backup flight control, parachute, GPS tracker)
### General Workflow


 1.  Identify the area, digitize/type the coords of 3 corners and the launching position
 2.  Adjust the flight parameters to your needs and generate flight control files
 3.  Convert and upload the mission control files either directly to your tablet/smartphone or alternatively  via the Litchi cloud.
 4.  Make an extensive preflight check
 5.  Fly the mission
## Installation


It is assumed that you are familiar with the R platform. Just go ahead and install the robubu package from github  using the [devtools](http://cran.r-project.org/package=devtools) package.

`<Code:R>`
devtools::install_github("gisma/robubu",ref="master")
`</Code>`

If you want to install all dependencies use:

`<Code:R>`
devtools::install_github("gisma/robubu",ref="master", dependencies = TRUE, force = TRUE)
`</Code>`

Note it is strongly recommended that you use a Linux platform. Nevertheless windows will probably work but Mac is not tested and won’t work most probably.

Additionally to R you must have installed at least GDAL SAGA GIS and GRASS GIS. For further information please refer to the [ Open Source GIS ](tutorials/softgis/intro) installation support pages.

##  

Training examples =====


The first example will introduce you to the basic usage and folder structure.

## Basic Example Phantom 3

 

Purpose: Survey flight over flat terrain to generate DSM and orthophoto. It is described for the Phantom3 and Litchi only. 

Addressed issues:

 1.  Create a reliable DSM for near surface retrieval of high resolution pictures
 2.  Create an orthophoto for visual inspection of POIs

### The short way


Digitize the 3 corner points of an area you want to map and  in addition as fourth point the position of the planned uav launch.  Save it to  *firstSurvey.json*. 


`<Code:R>`
 library(robubu)

 # preset = "uav" supress all not necessary tools
 leafDraw(mapCenter = c(50.855,8.691),preset="uav")

 # Use the digitized data and the example DEM to calculate a flight control file
 fp<-makeFP(rootDir="~/proj",
     workingDir="/drone/firstSurvey",
     missionName ="valleyWood",
     surveyArea="firstSurvey.json",
     flightAltitude =100,
     demFn = data(mrbiko))
`</Code>`

Note: The first two points determine the flight angle and direction the second and third coordinate determine the width of the area. 

If you want so save it on your SD card, open the [Litchi Mission](https///flylitchi.com/hub) website and click on the button ''Missions->Import''. Next navigate to the control file ''firstsurvey_1001.csv'' (you’ll find it in the folder ''~/projectDir/mission/control''). For exporting it choose ''Missions->Save'' and navigate/upload it to your missions subfolder of the Litchi app. That’s it.

Even more simple is the option to connect with the litchi cloud. While you are logged in with the same account it is synchronizing the data as soon as you start the litchi app.

### The long way


#### Digitizing of the survey area


We want to plan a flight in a more or less flat terrain in the upper Lahn-valley. First load the libraries and next start the small digitizing tool that is provided in ''robubu''. 

Note: you may take any other tool to digitize the survey area as well as you may type the coordinates on Stdin.

`<Code:R>`
# load robubu

library(robubu)

# start digitizing tool with preset = "uav" for a reduced toolbar

# see ?leafDraw for more information
leafDraw(mapCenter = c(50.855,8.691),preset="uav")
`</Code>`

{{ :rs:micrors:uavrs:leafdrwa.png?600 |}}

Feel free to digitize the four points needed:
 1.  P1,P2,P3 define the extend and angles of the mission area. 
 2.  P1 is the starting point of the survey
 3.  Flight direction angle and along distance is defined by P1->P2
 4.  P2->P3 defines the cross distance
 5.  P4 is the launching point. Try to digitize it very carefully because of getting an optimal launch altitude.

#### Some planning hints


 1.  If possible put the launching position somewhere (assumingly in the middle) of the proposed survey area with respect to a  optimal visibility to the uav and  the shortest possible distance for the radio controller to keep in contact to the uav.
 2.  It is helpful to fly ***along*** structures with the climbs at the end of each track. It save energy and in most cases the climbs can be visually controlled easier.
 3.  Try to identify your launching point//** very carefully**// and//** most reliable**//. The Phantom is taking this position as a home (reference) point for both position and altitude.
Finish digitizing and save it either as JS =JSON or KML file. Take care to use the correct extensions ''.json'' or ''.kml'' (the ''makeFP()'' function is requiring the correct extension).  In the current example save it as a json file named ''firstSurvey.json''.

### Calling makeFP

#### Working directories and other structural defaults

 
There are a lot of params to control the generation of an autonomous flight plan. In this first use case we keep it according to the issues of the task as simple as possible. First you some convenient params to organize the project as the project folder called ''~/proj/uav'' which is stored in ''projectDir''. The current working directory will be generated from the mission name and is always a subfolder of the ''projectDir''. So in this case it is set to ''firstSurvey''.  you will find in the resulting mission folder named ''~/proj/uav/firstsurvey'' two more subfolders. One is named ''control'' (for all control and log files) and the other is called ''run'' for all run time files that are generated during the analysis process.

Please note: additionally all used data files are copied to a folder called ''data'', which is located directly under the ''projectDir'' folder.

The project structure will look like the figure.

{{:rs:micrors:uavrs:structure.png |}}

 

#### Arguments used

''flightAltitude'' is set to the (legal) maximum of 100 m, ''flightPlanMode'' is set to ''track'' and finally a DEM of this area with 20m resulution is used to retrieve the altitude of the launching point. If we use the example data we first have to convert them to a valid GeoTiff file.

`<Code:R>`

data(mrbiko) # to use the example data it's easier to write same in tif format

writeRaster(mrbiko,"~/dem.tif")

fp<-makeFP(projectDir ="~/uav/cookbook",
           missionName ="firstSurvey",
           surveyArea="~/proj/drone/uniwald/myFirstSurvey.json",
           flightAltitude =100,
           maxSpeed =35,
           demFn ="~/dem.tif")
`</Code>`

The script generates:


*  R objects for visualisation

*  log file 

*  flight control file(s). 

All three of them are important even if a quick inspection of the generated objects is most of the time sufficient. The log file dump summarize the most import params, as the calculated speed and picture rate based on an estimation of the mission time. In general you can say as higher you fly as faster you can go. The flight time will significantly increase with each 10 meter lowering the flight altitude. 

`<Code:bash>`
[1]"[ 2016-09-26 23:17:26 ] INFO ----- use the following mission params! ------- " 
[1]"[ 2016-09-26 23:17:26 ] INFO set RTH flight altitude to  :  100  (m) " 
[1]"[ 2016-09-26 23:17:26 ] INFO set mission speed to a max of:  35  (km/h)  "
[1]"[ 2016-09-26 23:17:26 ] INFO set pic rate to at least :  5.3  (sec/pic)  "
[1]"[ 2016-09-26 23:17:26 ] INFO calculated mission time  :  12.2  (min)  "
[1]"[ 2016-09-26 23:17:26 ] INFO estimated battery liftime  :  10  (min)  "
[1]"[ 2016-09-26 23:17:26 ] INFO Area covered  :  37.2799964578867  (ha) "

NOTE 1: flighttime > battery lifetime! control files have been splitted.HaveFun... 
NOTE 2:You will find all parameters in the logfile:~/uav/cookbook/firstSurvey/control/firstSurvey_100.log  
`</Code>`

Using ''mapview()'' you can easily visualize the result. You see the footprints of the images (blue), surveyArea(red), turnpoints of track (blue circles), launch position (red). 

`<Code:R>`
mapview(fp[5](5),color="red", alpha.regions =0.1,lwd=0.5)+
mapview(fp[1](1),zcol ="altitude",lwd=1,cex=4)+
mapview(fp[3](3),color="red",cex=5)+
mapview(fp[4](4),color="darkblue", alpha.regions =0.1,lwd=0.5)
`</Code>`

{{ :rs:micrors:uavrs:mapview.png?600 |}}

Just for your interest the resulting basic control file is named ''firstSurvey_1001.csv'' and looks (DJI) like this:

`<Code:R>`
latitude,longitude,altitude,heading,curvesize,rotationdir,gimbalmode,gimbalpitchangle,actiontype1
50.8562700012854,8.67969274520874,100,61.3278866905878,0,0,0,-90,0.6
50.8562397243629,8.67955902673377,100,61.3278866905878,0,0,0,-90,0.6
50.854739330123,8.67293357849121,100,61.3278866905878,0,0,0,-90,0.6
50.854739330123,8.67293357849121,100,61.3278866905878,0,0,0,-90,0.6
50.8550343329483,8.67378583665562,100,61.3278866905878,0,0,0,-90,0.6
50.8553293357587,8.67463810019652,100,61.3278866905878,0,0,0,-90,0.6
50.855624338554,8.67549036911401,100,61.3278866905878,0,0,0,-90,0.6
50.8559193413343,8.67634264340815,100,61.3278866905878,0,0,0,-90,0.6
50.8562143440996,8.67719492307906,100,61.3278866905878,0,0,0,-90,0.6
`</Code>`

If you ever forget what you did you will find a log file with the whole logging history of the mission called ''firstSurvey_100'' in the ''control'' directory.
### Export to the flight app


Open [Litchi Mission](https///flylitchi.com/hub) and click on the button ''Missions->Import'' and navigate to the control file firstSurvey_1001.csv. To export it click ''Missions->Save''. If you need to export the files offline you can use this [workaround](rs/micrors/uavrs/dji/litchihub).


{{ :rs:micrors:uavrs:litchihub.png?600 |}}

Ready to take off - that’s the first flight plan. 




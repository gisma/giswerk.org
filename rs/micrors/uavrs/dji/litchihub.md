---
layout: liquibase
lang: en
---
# Offline use of the Litchi mission hub

The third party software [Litchi](https///flylitchi.com/) provides an interface to the DJI Phantom and Inspire models. In addition to the typical derivatives like apps for android and ios and a cloud based tool Litchi provides an interface to user generated csv/kml waypoint flight control data.

Unfortunately this website is heavily utilizing the Google map API which makes it fairly cumbersome to use it offline without a connection to the internet. A simple workaround using Google Chrome can overcome this shortcoming. Chrome offers the possibility to reload cached websites in a regular way.

Depending on the Chrome version you use type [chrome://flags](chrome///flags) in the address box and look for either ''offline load stale'' or ''show saved copy'' flag. You have to enable one of these options and restart the browser. If you navigate now offline to the [litchi hub](https///flylitchi.com/hub) You will notice a new button that appear that lets you load the cached version.

`<note important>`Don't forget that you have visited the litchi hub start page with a working internet connection and preferably in your target area. If not there will be nothing cached what you might want to use when you are sitting offline in the woods.`</note>`



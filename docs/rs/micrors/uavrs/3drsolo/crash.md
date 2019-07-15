---
layout: liquibase
lang: en
---

# Failed FW Update, Factory Reset...

The Solo has inside two SD Cards, one for the flight controller and one for the system.  A factory reset or a firmware update can go wrong due to a write error on the SD card of the Controller or the card inside Solo. Usually the SD card is damaged and useless afterwards. This would be no problem if only one could  take the SD card and push a new image on it. But first you have to [tear down](https///www.youtube.com/watch?v=5jzKOa2lz-g) the whole Solo hardware including the flight controller. Second you have to cut the glued SD card which is a fairly fumbling job and finally you nee the images for flashing the two SD cards. Just to complete this weird story: You are loosing all warranties and there was know help ever from the 3DR team. 

If you have disassembled the Solo you just need to push the images on a new SD card and reassable the whole thing.  

Assuming you have the downloaded image at ''~/proj/drone/3DR/image/'' and it is named ''mmcblk0_Solo'' you can easily push it to the SD Card with the following command.


`<code:bash>`
# Solo image (SD Card from the flight controller of the Solo)

sudo dd if=~/proj/drone/3DR/image/mmcblk0_Solo of=/dev/mmcblk0

# controller image (SD card from the ardoo RC controller)

sudo dd if=~/proj/drone/3DR/image/mmcblk0 of=/dev/mmcblk0
`</code>`

In most cases you need to fix the flight controller of the Solo. When you repair the connection manually you may avoid disassembling the Artoo controller and just fix one image. 

For getting the images and more information you have to contact the Facebook Group [3DR Solo Hack](https///www.facebook.com/groups/363840837156620/) or contact  --- //[Christoph Reudenbach](reudenbach@staff.uni-marburg.de)//

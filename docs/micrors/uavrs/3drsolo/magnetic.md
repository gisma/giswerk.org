---
layout: default
title: Customization
nav_order: 4
---
# Magnetic Interferences

Besides the poor GPS antenna the ''magnetic interferences'' is an central issue of the 3DR Solo that can drive you crazy. 

Sometimes the compass is disturbed by metal etc. However in case of receiving all the times the error message ''magnetic interferences'' it is in most cases an parameter setup failure that is probably caused by a firmware update or a failure using external flight control software.

In this case set the parameter ''SYSID_SW_MREV'' to ''0''. After doing so re-calibrate the sensors and it should work.


# Mac Pro Mini Hackintosh

## Goal
My goal was to build a Hackintosh that has a smaller footprint than the 2019 Mac Pro but also just as powerful if not more powerful. I've been using a 2012 Macbook Pro that is still running strong but I wanted much more power to do video/photo editing, mobile app development, and some machine learning. Seeing that Apple came out with a very pricey version of the Mac Pro that starts out at $6K, I basically laughed at that idea of buying one. Having been a long time lurker of the Hackintosh movement I decided to jump into the pool after hearing about the success people were having with the OpenCore Vanilla Guide plus the use of AMD CPU's.

## Objective
In this "Guide" I'm not going to go over every step of the build but will point you to resources that I used and thought were very helpful. Keep in mind that depending on the hardware you go with the experience and process may be slightly different.

## The Build

* **OpenCore:** 0.5.9
* **CPU:** AMD Ryzen 9 3950X
* **Motherboard:** Gigabyte X570i AORUS PRO WIFI
* **Memory:** Corsair Vengeance LPX Pro 2x32GB = 64 GB DDR4-3600MHz
* **Video Card:** Gigabyte Radeon RX 5700 XT 8 GB GAMING OC
* **Storage (macOS):** Sabrent Rocket 1 TB NVMe 4.0 M.2 SSD
* **Storage (media):** Sabrent Rocket 1 TB NVMe 4.0 M.2 SSD
* **Wireless/Bluetooth:** Broadcom BCM94360NG
* **Case/Cooler/Power:** NZXT H1

## Kexts
* AppleALC
* WhateverGreen
* Lilu
* VirtualSMC
* smalltreeintel82576

## Benchmarks

_All values are the average of three runs_

* [Geekbench 5](https://www.geekbench.com/)
  * Single Core: 
  * Multicore: 
  * OpenCL: 
  * Metal: 
* [LuxMark LuxBall](http://www.luxmark.info/): 
* [BruceX](https://blog.alex4d.com/2013/10/30/brucex-a-new-fcpx-benchmark/):  seconds
* [Cinebench R20](https://www.maxon.net/en-us/products/cinebench-r20-overview/): 
* [Blackmagic Disk Speed Test](https://apps.apple.com/us/app/blackmagic-disk-speed-test/id425264550) (Samsung 970 Evo)
  * Read:  MB/s
  * Write:  MB/s
  
## What Works

* **The System, It Boots, and Works!**
* **CPU:** While this works it's not benchmarking where it should be. Did I lose in the silicon lottery?
* **AirDrop Handoff:** I replaced the Intel card with the Broadcom CM94360NG
* **Adobe Products:** Lightroom, Photoshop, all work but required some hacking
* **Shutdown:** Sort of works but requires that I turn wifi off before shutdown otherwise it will restart/boot back up
* **USB:** All works
* **GPU:** AMD plug & play however see below about HEIC images
* **LAN:** Works just fine but needs the right kext
* **Final Cut Pro:** Works just fine

## What Doesn't Work

* **HEIC**: HEIC Images appears to have issues. Big pixalated boxes on the dynamic wallpaper and image preview. Likely an issue with 5700XT GPU.
* **Sleep/Wake**: have not solved for this yet. Not a big deal just...

## Issues

[See the GitHub repository issues tracker](https://github.com/armanijohnny/MacProMiniHackintosh/issues)

## Resources
* [**OpenCore**](https://dortania.github.io/OpenCore-Desktop-Guide/) 

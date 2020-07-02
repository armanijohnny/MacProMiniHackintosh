# Mac Pro Mini Hackintosh

## Goal
My goal was to build a Hackintosh that has a smaller footprint than the 2019 Mac Pro but also just as powerful if not more powerful. I've been using a 2012 Macbook Pro that is still running strong but I wanted much more power to do video/photo editing, mobile app development, and some machine learning. 

Seeing that Apple came out with a very pricey version of the Mac Pro that starts out at $6K, I basically laughed at that idea of buying one. Having been a long time lurker of the Hackintosh movement I decided to jump into the pool after hearing about the success people were having with the OpenCore Vanilla Guide plus the use of AMD CPU's.

In this "Guide" I'm not going to go over every step of the build but will point you to resources that I used and thought were very helpful. Keep in mind that depending on the hardware you go with the experience and process may be slightly different.

## The Build

* **OpenCore:** 0.5.9
* **Mac OS:** Catalina 10.15.5
* **CPU:** AMD Ryzen 9 3950X
* **Motherboard:** Gigabyte X570i AORUS PRO WIFI
* **Memory:** Corsair Vengeance LPX Pro 2x32GB = 64 GB DDR4-3600MHz
* **Video Card:** Gigabyte Radeon RX 5700 XT 8 GB GAMING OC
* **Storage (macOS):** Sabrent Rocket 1 TB NVMe 4.0 M.2 SSD
* **Storage (media or dual boot):** Sabrent Rocket 1 TB NVMe 4.0 M.2 SSD (Still deciding if I want to use this to boot Windows)
* **Wireless/Bluetooth:** Broadcom BCM94360NG
* **Case/Cooler/Power:** NZXT H1

When it comes to parts there's a few things you have to consider and think about. 
CPU: Prior to OpenCore Intel was the name of the game. However with OpenCore it's pretty easy to use an AMD chip. 
GPU: AMD is whats supported natively on MAC's and straight up plug play with no fuss. If you go with a 5000 series AMD GPU you'll need to add one extra Boot Arg to your plist
WIFI/BT: If you want this to have Airdrop and Handoff you need a Broadcom card. In my case a Broadcom BCM94360NG.
Thunderbolt: If you want this you'll want to go Intel CPU with a mobo like a Z390 or you add a Titan Ridge TB card. At the moment I dont think AMD supported motherboard actually works.  


## Start Here...

If you want to take this seriously the [OpenCore guide](https://dortania.github.io/OpenCore-Desktop-Guide/) has all the steps to building your hackintosh. Read it line by line as you are going through it'll make sense. 

If you are more of a visual person that just rather learn as you go I suggest watching a few of [Technolli Youtube](https://www.youtube.com/c/TechNolli/videos) video's of various hackitosh builds he has put together for his subscribers. Literally he goes from start to finish. Building the computer, creating the bootloader, creating your EFI, walking through OpenCore, and installing it all on your new build. 

The reason why I chose the NZHT H1 case was because of many reasons. 1) Form Factor, Design, and Size 2) AIO liquid cooling, case fans, all included and pre-configured 3)Power supply comes with it 4) Super easy to install everything! Last time I built a computer was probably 20 years ago back in college and this was just a breeze. Here's a handy video of the NZXT H1 build using the same motherboard that I used that came in handy. [Robeytech NZXT H1 Build](https://youtu.be/0tNqpVc-B9A)

## Tools Needed

* [OpenCore](https://github.com/acidanthera/OpenCorePkg/releases/) - Tool to turn your PC into a Hackintosh
* [GibMacOS](https://github.com/corpnewt/gibMacOS) - Script to download MacOS for Bootloader
* [ProperTree](https://github.com/corpnewt/ProperTree) - GUI plist editor
* [MaciASL](https://bitbucket.org/RehabMan/os-x-maciasl-patchmatic/downloads/) - AML(ACPI Machine Language) compiler and IDE 
* [Mount EFI](https://github.com/corpnewt/MountEFI) - Mount the EFI from the bootloader and system drive so you can add files to it
* [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) - Generate SMBIOS Serial Number
* [USB Stick](https://amzn.to/38mfhUB) - For the bootloader. Minimum space needed at least 10GB. Must be formated so don't use and existing one with data you want to keep.
* [Computer Tools for building computer](https://amzn.to/3ge7hHY) - Screw drivers and etc.

## Bootloader
This is what you need to create on a formated USB drive(minimum 10GB)  with the MacOS of your choice and the EFI with all the drivers, kext, plist, and etc to get your new Hackitosh running. You can create the bootloader from a Mac or a Windows PC. This is also where you'll need to download [GibMacOS](https://github.com/corpnewt/gibMacOS) so you can get a copy of the MacOS of your choice.

Insturctions on how to go about it here: [OpenCore Creating USB Bootloader](https://dortania.github.io/OpenCore-Desktop-Guide/installer-guide/)
Video of how to do it: [Windows Version](https://www.youtube.com/watch?v=01q4M91_fK4)  or [Mac Version](https://www.youtube.com/watch?v=97C1Rsarto8)

## OpenCore for Ryzen
You'll now need to download the [latest OpenCore](https://github.com/acidanthera/OpenCorePkg/releases/) then start building your EFI folder. You'll also need [Mount EFI](https://github.com/corpnewt/MountEFI) so you can reach the EFI folders.  

Instructions: OpenCore Adding 
Video of how to build the EFI folder that needs to be loaded onto the Bootloader: [Technolli Easy OepnCore for Ryzen](https://www.youtube.com/watch?v=UDY0PsCEHx8)


## Drivers

* [HfsPlus.efi](https://github.com/acidanthera/OcBinaryData/blob/master/Drivers/HfsPlus.efi) - Needed for seeing HFS volumes
* OpenRuntime.efi - Included in OpenCore. Helps with patching boot.efi for NVRAM fixes and better memory management.

## Kexts

* [VirtualSMC](https://github.com/acidanthera/VirtualSMC/releases) - Emulates the SMC chip found on real macs, without this macOS will not boot
* [Lilu](https://github.com/vit9696/Lilu/releases) - A kext to patch many processes, required for AppleALC, WhateverGreen, VirtualSMC and many other kexts. Without Lilu, they will not work.
* [AppleALC](https://github.com/vit9696/AppleALC/releases) - Used for AppleHDA patching, used for giving you onboard audio. Ryzen/Threadripper systems rarely have mic support
* [WhateverGreen](https://github.com/acidanthera/WhateverGreen/releases) - Used for graphics patching DRM, boardID, framebuffer fixes, etc, all GPUs benefit from this kext.
* [smalltreeintel82576](https://github.com/khronokernel/SmallTree-I211-AT-patch/releases) - Ethernet for this motherboard to work. Required for I211 NICs, based off of the SmallTree kext but patched to support I211

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
* **Adobe Products:** Lightroom, Photoshop, all works but required some hacking
* **Shutdown:** Sort of works but requires that I turn wifi off before shutdown otherwise it will restart/boot back up
* **USB:** All works
* **GPU:** AMD plug & play however see below about HEIC images
* **LAN:** Works just fine but needs the right kext
* **Final Cut Pro:** Works just fine

## What Doesn't Work

* **HEIC**: Sometimes HEIC Images appears to have issues. Big pixalated boxes on the dynamic wallpaper and image preview. Likely an issue with 5700XT GPU.
* **Sleep/Wake**: have not solved for this yet. Not a big deal just...

## Issues

[See the GitHub repository issues tracker](https://github.com/armanijohnny/MacProMiniHackintosh/issues)

## Resources
* [**OpenCore**](https://dortania.github.io/OpenCore-Desktop-Guide/)
* [**Technolli**](https://www.youtube.com/c/TechNolli/videos) 
* [**r/Hackintosh subreddit**](https://www.reddit.com/r/hackintosh/)
* [**TonyMacX86**](https://www.tonymacx86.com/)
* [**Robeytech NZXT H1 Build**](https://youtu.be/0tNqpVc-B9A)

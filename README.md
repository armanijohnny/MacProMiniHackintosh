# Mac Pro Mini Hackintosh aka iHack Pro

![Image of Hackintosh Working](https://preview.redd.it/zqeejpikdp951.png?width=1920&format=png&auto=webp&s=cd0bd197771731c8780bdc3f09fc124451d2c9ee)
*(It works! I've since updated from iMacPro1,1 to MacPro7,1 and upgraded to Catalina 15.15.6)*

My goal was to build a Hackintosh that has a smaller footprint than the 2019 Mac Pro but also just as powerful if not more powerful. I've been using a 2012 Macbook Pro that is still running strong but I wanted much more power to do video/photo editing, mobile app development, and some machine learning. 

Seeing that Apple came out with a very pricey version of the Mac Pro that starts out at $6K, I basically laughed at that idea of buying one. Having been a long time lurker of the Hackintosh movement I decided to jump into the pool after hearing about the success people were having with the OpenCore Vanilla Guide plus the use of AMD CPU's.

In this "Guide" I'm not going to go over every step of the build but will point you to resources that I used and thought were very helpful. Keep in mind that depending on the hardware you go with the experience and process may be slightly different.

## The Build
![Image of Build Components](https://preview.redd.it/bq9ywx9vcp951.jpg?width=4032&format=pjpg&auto=webp&s=f48ae5ada572f37fa5f8befb6f55aeb7c1e8f5ea)

* **OpenCore:** 0.5.9
* **Mac OS:** Catalina 10.15.6
* **SMBIOS:** MacPro7,1
* **CPU:** [AMD Ryzen 9 3950X](https://amzn.to/3gnfCcr)
* **Motherboard:** [Gigabyte X570i AORUS PRO WIFI](https://amzn.to/38wQtti)
* **Memory:** [Corsair Vengeance LPX Pro 2x32GB = 64 GB DDR4-3600MHz](https://amzn.to/3eXKIap)
* **Video Card:** [Gigabyte Radeon RX 5700 XT 8 GB GAMING OC](https://amzn.to/2YWSpb7)
* **Storage (macOS):** [Sabrent Rocket 1 TB NVMe 4.0 M.2 SSD](https://amzn.to/3irGee6)
* **Storage (media or dual boot):** [Sabrent Rocket 1 TB NVMe 4.0 M.2 SSD](https://amzn.to/3irGee6) (Still deciding if I want to use this to boot Windows)
* **Wireless/Bluetooth:** [Broadcom BCM94360NG](https://amzn.to/38rbMMU)
* **Case/Cooler/Power:** [NZXT H1](https://www.nzxt.com/products/h1-matte-black)

**When it comes to parts there's a few things you have to consider and think about.**    

**CPU:** Prior to OpenCore Intel was the name of the game and considered native. However with OpenCore it's pretty easy to use an AMD chip.  

**GPU:** AMD is what's supported natively on MAC's and straight up plug play with no fuss. If you go with a 5000 series AMD GPU you'll need to add one extra Boot Arg to your plist which is easy and in my config.plist. I have encountered issues with the 5700 XT which are described below.  

**WIFI/BT:** If you want this to have Airdrop and Handoff you need a Broadcom card. In my case a Broadcom BCM94360NG.  

**Thunderbolt:** If you want this you'll want to go Intel CPU with a mobo like a Designare Z390 or you add a Titan Ridge TB card. At the moment I dont think AMD supported motherboard actually works.  

**RAM:** With any computer build check the motherboards list of acceptable Ram otherwise you'll be wasting money.


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

**Additional Tools**

* Patience
* Google Search
* Navigating Forums
* Following in detail OpenCore guide

## Bootloader
This is what you need to create on a formated USB drive(minimum 10GB)  with the MacOS of your choice and the EFI with all the drivers, kext, plist, and etc to get your new Hackitosh running. You can create the bootloader from a Mac or a Windows PC. This is also where you'll need to download [GibMacOS](https://github.com/corpnewt/gibMacOS) so you can get a copy of the MacOS of your choice.

Insturctions on how to go about it here: [OpenCore Creating USB Bootloader](https://dortania.github.io/OpenCore-Desktop-Guide/installer-guide/)
Video of how to do it: [Windows Version](https://www.youtube.com/watch?v=01q4M91_fK4)  or [Mac Version](https://www.youtube.com/watch?v=97C1Rsarto8)

## OpenCore for Ryzen
You'll now need to download the [latest OpenCore](https://github.com/acidanthera/OpenCorePkg/releases/) then start building your EFI folder. You'll also need [Mount EFI](https://github.com/corpnewt/MountEFI) so you can reach the EFI folders.  

**Instructions:**
Follow the OpenCore guide will be key. If you wish to check out a video a link is below.
* [Adding The Base OpenCore Files](https://dortania.github.io/OpenCore-Desktop-Guide/installer-guide/opencore-efi.html)  
* [Gather Kext & Drivers](https://dortania.github.io/OpenCore-Desktop-Guide/ktext.html) - A copy of my [EFI is located here](link to EFI folder)  
* [ACPI](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-EC-USBX-DESKTOP.aml) - This is all I needed  
* [Config.plist Setup](https://dortania.github.io/OpenCore-Desktop-Guide/config.plist/)  
* [AMD Zen Config.plist](https://dortania.github.io/OpenCore-Desktop-Guide/AMD/zen.html)
* [Patches.plist](https://github.com/AMD-OSX/AMD_Vanilla/tree/opencore/17h) - AMD Kernal patching

**Video:** Great video on how to build the EFI folder that needs to be loaded onto the Bootloader: [Technolli Easy OepnCore for Ryzen](https://www.youtube.com/watch?v=UDY0PsCEHx8)

**Installation**
After loading all the neccessary items into the EFI folder onto your bootloader USB you are ready to Install it onto your PC. You'll want to go into the bios first to make some updates which the video below can explain what needs to be updated. 

**Instructions:** [Installation](https://dortania.github.io/OpenCore-Desktop-Guide/installation/installation-process.html)  
**Video:** [Technolli Easy OpenCore for Ryzen Install](https://youtu.be/UDY0PsCEHx8?t=1272)  

## BIOS Settings

You'll want to go into your BIOS by restarting the computer and just hitting Delete until BIOS comes up. Just make sure that using the X570I motherboard that these settings are in place. XMP is not needed to be updated but from what I can tell the ram was not taking full advantage until I updated this setting. Also probably suggest to update your BIOS version as well just in case they come out with any new updates or improvements. 

* Load Optimized Defaults
* Above 4G Decoding - Disabled
* CSM Support - Disabled
* Extreme Memory Profile XMP - Profile 1
* PCIe Slot Configuration - Gen3 (If you encounter issues with your system freezing up during Setup, After login, or in general and have a 5700XT paired with this board you'll need to switch it from Auto to Gen3 to get it stable. This also resolved my issues with the HEIC images/Dynamic Wallpaper being big block pixelated)

## Drivers

* [HfsPlus.efi](https://github.com/acidanthera/OcBinaryData/blob/master/Drivers/HfsPlus.efi) - Needed for seeing HFS volumes
* OpenRuntime.efi - Included in OpenCore. Helps with patching boot.efi for NVRAM fixes and better memory management.

## Kexts

* [VirtualSMC](https://github.com/acidanthera/VirtualSMC/releases) - Emulates the SMC chip found on real macs, without this macOS will not boot
* [Lilu](https://github.com/vit9696/Lilu/releases) - A kext to patch many processes, required for AppleALC, WhateverGreen, VirtualSMC and many other kexts. Without Lilu, they will not work.
* [AppleALC](https://github.com/vit9696/AppleALC/releases) - Used for AppleHDA patching, used for giving you onboard audio. Ryzen/Threadripper systems rarely have mic support
* [WhateverGreen](https://github.com/acidanthera/WhateverGreen/releases) - Used for graphics patching DRM, boardID, framebuffer fixes, etc, all GPUs benefit from this kext.
* [smalltreeintel82576](https://github.com/khronokernel/SmallTree-I211-AT-patch/releases) - Ethernet for this motherboard to work. Required for I211 NICs, based off of the SmallTree kext but patched to support I211
* [SMCAMDProcessor](https://github.com/trulyspinach/SMCAMDProcessor) - All the tools for CPU power and Temprature out there are made for Windows. There's nothing for Mac's with AMD since the real Mac's don't have AMD. I found this tool that allows for you to manage the power and monitor the AMD CPU. Once installed iStat's pro now reads the temp and they have a nice app that has much more data and management.
* [MacProMemoryNotificationDisabler](https://github.com/IOIIIO/MacProMemoryNotificationDisabler/releases/) - Fix the "too much memory" error in the Memory tab of About This Mac. Typically when you use SMBIOS MacPro7,1

## ACPI  

* [ACPI](https://dortania.github.io/Getting-Started-With-ACPI/) - What I only needed for this build [SSDT-EC-USBX-Desktop.aml](https://github.com/dortania/Getting-Started-With-ACPI/blob/master/extra-files/compiled/SSDT-EC-USBX-DESKTOP.aml). These are tables present in your firmware that outline hardware devices like USB controllers, CPU threads, embedded controllers, system clocks and such.

## Benchmarks

Just looking at Geekbench 5 numbers on the single core level it beats out all the Macs that Apple sells(iMac Pro, Mac Pro, Macbook Pro, and etc). On the multicore level it benchmarks between the Mac Pro 16 core and the Mac Pro 12 Core. However either there is some issue with how Geekbench works, the CPU, or the parts I've used but in theory and based on all the benchmarks I've seen from others the multicore on a 3950X should come in over 14,000~ in line with the Mac Pro 16 core. I've used SMCAMD tool to better gauge temprature and core usage and all appears normal.

On the other hand using more real life benchmarks such as Cinebench, Blender, BruceX this thing is an absolute beast and performs just where the Ryzen 9 3950X should perform if not better in some cases. So overally yeah it totally matches the Mac Pro.

* [Geekbench 5](https://www.geekbench.com/)
  * Single Core: 1,332
  * Multicore: 12,934 (Still need to figure out why it's not closer to 14K~)
  * OpenCL: 52,439
  * Metal: 55,524
* [Cinebench R20](https://www.maxon.net/en-us/products/cinebench-r20-overview/): 9,361
* [Blender Benchmark](https://opendata.blender.org/)
  * bmw27: 1:14
  * classroom: 3:37
  * fish_cat: 1:52
  * koro: 2:38
  * pavillon_barcelona: 3:57
  * victor: 8:35
* [BruceX](https://blog.alex4d.com/2013/10/30/brucex-a-new-fcpx-benchmark/): 14.73 seconds
* [Blackmagic Disk Speed Test](https://apps.apple.com/us/app/blackmagic-disk-speed-test/id425264550)
  * Read:  MB/s 5,000~
  * Write:  MB/s 4,400~
  
## What Works

* **The System, It Boots, and Works Just Like a Mac!**
* **CPU:** While this works it's not benchmarking where it should be. Did I lose in the silicon lottery?
* **AirDrop Handoff:** I replaced the Intel card with the Broadcom CM94360NG
* **Adobe Products:** Lightroom, Photoshop, all works but required some [hacking](https://gist.github.com/naveenkrdy/26760ac5135deed6d0bb8902f6ceb6bd)
* **Shutdown:** Sort of works but requires that I turn wifi off before shutdown otherwise it will restart/boot back up
* **USB:** All works
* **GPU:** AMD plug & play. I needed to update bios so that the PCIE instead of Auto I switched to Gen3 and everything is now stable.
* **LAN:** Works just fine but needs the right kext
* **Final Cut Pro:** Works just fine
* **Audio:** Top headphone jack works. I plan on using a USB for my DAC.  

## What Doesn't Work

![Image of Pixalated Wallpaper](https://preview.redd.it/vy7d1osodp951.png?width=1912&format=png&auto=webp&s=444be5fcff163627662d7c9ab384baa804b9ed25)
*(HEIC/Dynamic Wallpaper issue. Update 7/20/2020 Issue is now Resolved :-)*

* **HEIC: [RESOLVED]** Sometimes HEIC Images appears to have issues. Big pixalated boxes on the dynamic wallpaper and image preview. Likely an issue with 5700XT GPU. **7/19/2020** Finally figured out the issue and how to resolve it. I needed to update the BIOS for the PCIE from Auto -> Gen3. No more issues with HEIC images. In BIOS -> Advanced Mode -> Settings -> Miscellaneous -> PCIe Slot Configuration -> Change from Auto to Gen3 and that's it.
* **Sleep/Wake**: Have not solved for this yet. This issue is very likley due to USB configuration. I'll try to properly assign the USB ports and see if that works. 
* **System Freeze Sometimes: [RESOLVED]** This is the [Kernal Panic Error](https://pastebin.com/qhKFQh8D) that I am seeing. After synching my Apple account, iCloud, Photos, and etc when the system is idle it freezes/crash but does not reboot. When I look into the crash logs I see VTDecoderXPCService. I think what may be happening is that the system is analysing all the iCloud photos/videos plus the 5700 XT is having some issues there and causes the VTDecoderXPCService kernel panic. This seems to happen when the machine starts to go into a low power state before sleep(even though I have sleep turned off) and the MacOS AMD kexts cause a panic. I guess it happens in the real [Mac Pro with 5700 XT GPU](https://www.reddit.com/r/macpro/comments/eecm69/mac_pro_2019_kernel_panic_with_5700_xt_installed/). Here's another thread about this [issue in real Mac Pro with the 5700 XT](https://forums.macrumors.com/threads/amd-radeon-rx-5700.2189066/page-7). Until Catalina or Big Sur adds 5700 XT in their list it might be an on going issue. Word has it if you use SMBIOS of iMac19,1 you don't encounter these VTDecoderXPCService kernal panic [Link](https://www.reddit.com/r/hackintosh/comments/f7ixji/yet_another_louqe_ghost_s1_success_story_opencore/) An alternative is to go with an older Radeon GPU like the 580 or Vega.

   It appears this system freeze/crash may not be an issue with the 5700 XT but more of a Catalina issues. There's a [whole thread of people](https://forums.macrumors.com/threads/constant-kernel-panics-userspace-watchdog-timeout-no-successful-checkins-from-com-apple-windowserver.2222878/) with real Macs having similar issues. **[Solution]** So I found this [thread on AMD-OSX](https://amd-osx.com/forum/viewtopic.php?t=10025) and it did support my theory that it was Photos that was causing the system to crash. I simply moved my photo library out of the pictures folder and into the trashbin to test and the freezing/crash issue stopped. Let the machine run so the monitor could turn off and I was able to log back in just fine. I wonder if the process actually finishes analyzing all my photos/videos if there would still be this issue with smaller batches of images and photos being added/synched. I would love to have Photo's but until Apple comes up with a fix I may scrap it or I'll try to have the Photo's library on my 2nd M.2 drive that is designated for media or perhaps on my NAS. I'll report back and see but for now the system stopped crashing.
    
    **Update 7/05/2020: Work Around Solution** So I tested out my theory by creating a Photo's library on my NAS but the problem with that as I found out is that Photo's don't work on the NAS if I want to synch it with iCloud. However with my secondary Sabrent 1TB M.2 (now diesignated as my media drive) I created a new Photo's library on there and was able to synch my iCloud and it had no issues with freezing the system and successfully analyse all the videos and photos. So looks like i found my solution.
    
    **Update 7/07/2020:** So it seems like this is still not exaclty resolved/worked. I got the same panic error today while I was transfering a bunch of videos over from my DJI Osmo. It's possible the Photos was running it's analyses in the background again. I got the same Kernal Panic as I did before https://pastebin.com/qhKFQh8D. So it seems that this is a big problem on legit machines and not just hackintosh.  
    
    **Update 7/19/2020 [Resolved]** I had major issues with freezing and I think I solved that by updating the BIOS Settings for the PCIE from Auto to Gen3 for the GPU. This seemed to have keep things stable and with no crashing! So if you are using a similar motherboard and GPU as mine try this in the BIOS: In BIOS -> Advanced Mode -> Settings -> Miscellaneous -> PCIe Slot Configuration -> Change from Auto to Gen3 and that's it. This solved all my issues with the system freezing. I even had it scan my 101GB worth of icloud Photos library with no issues. Also the issues with HEIC/Dynamic wallpaper went away as well. No more freezing while left idle. 

## Issues

[See the GitHub repository issues tracker](https://github.com/armanijohnny/MacProMiniHackintosh/issues)

## My Thoughts

![Image of Pixalated Wallpaper](https://preview.redd.it/t2t96tkhd2c51.jpg?width=4032&format=pjpg&auto=webp&s=9c02d95d49c384a89c4345c376b713135dc13908)
*The Build (updated to MacPro7,1 and running Catalina 10.15.6)*  

**Was it worth it?** Heck yeah it was worth it. I got to build a badass computer and learn how to hack it.  

**What about the issues?** I kind of expected it and give me some time I should be able to solve for it. H̶E̶I̶C̶ ̶a̶n̶d̶ ̶S̶y̶s̶t̶e̶m̶ ̶f̶r̶e̶e̶z̶e̶ ̶s̶e̶e̶m̶ ̶t̶o̶ ̶b̶e̶ ̶r̶e̶l̶a̶t̶e̶d̶ ̶t̶o̶ ̶5̶7̶0̶0̶ ̶X̶T̶ ̶s̶o̶ ̶I̶ ̶m̶a̶y̶ ̶l̶o̶o̶k̶ ̶t̶o̶ ̶g̶o̶ ̶w̶i̶t̶h̶ ̶a̶n̶o̶t̶h̶e̶r̶ ̶G̶P̶U̶ ̶l̶i̶k̶e̶ ̶t̶h̶e̶ ̶V̶e̶g̶a̶,̶ ̶5̶8̶0̶,̶ ̶o̶r̶ ̶V̶I̶I̶ ̶o̶r̶ ̶j̶u̶s̶t̶ ̶w̶a̶i̶t̶ ̶i̶t̶ ̶o̶u̶t̶ ̶u̶n̶t̶i̶l̶ ̶A̶p̶p̶l̶e̶ ̶h̶a̶s̶ ̶b̶e̶t̶t̶e̶r̶ ̶s̶u̶p̶p̶o̶r̶t̶ ̶f̶o̶r̶ ̶t̶h̶e̶s̶e̶ ̶c̶a̶r̶d̶s̶.̶ ̶ Update: 7/20/20 Now that I've have the 5700 XT GPU issues resolved this system is just badass! 

**Am I worried that Apple is going to be usng their ARM Chips?** As noted in their conference they intend to continue using Intel for awhile and supporting them for many many years. Plus the hackintosh community is very robust. Even to this day people can still jailbreak their iPhones and Apple I'm sure have tried to stop that.  

**How much was the build?** I'll have to total it all up but probably around $2,100~. Still this is amazing when the Mac Pro it benches against is around $9K!  

## Resources
* [**OpenCore**](https://dortania.github.io/OpenCore-Desktop-Guide/)
* [**Technolli**](https://www.youtube.com/c/TechNolli/videos) 
* [**r/Hackintosh subreddit**](https://www.reddit.com/r/hackintosh/)
* [**AMD OSX**](https://forum.amd-osx.com/index.php)
* [**TonyMacX86**](https://www.tonymacx86.com/)
* [**Robeytech NZXT H1 Build**](https://youtu.be/0tNqpVc-B9A)

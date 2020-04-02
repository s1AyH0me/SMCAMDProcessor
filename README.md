SMCAMDProcessor & AMDRyzenCPUPowerManagement
========

XNU kernel extension for AMD processor power management and monitoring.
Also comes with a plugin for [VirtualSMC](https://github.com/acidanthera/VirtualSMC) to export readings to other application.

Please note that this release is at very initial stage of development, make sure you have a proper backup of your EFI folder and never run on any system that matters. 

## Installation

SMCAMDProcessor now comes in two separate binary(kernel extension):
* AMDRyzenCPUPowerManagement.kext for all power management features. This kext is also required if you would like to use AMD Power Gadget.
* SMCAMDProcessor.kext to publish readings to [VirtualSMC](https://github.com/acidanthera/VirtualSMC), which enables macOS applications like iStat to display sensor data. This kext depends on AMDRyzenCPUPowerManagement.kext to collect sensor data, thus must be loaded after.

1. Download the kext(s) and application from [Release](https://github.com/trulyspinach/SMCAMDProcessor/releases) page
2. Add AMDRyzenCPUPowerManagement.kext to kext folder of your bootloader.
3. Edit your bootloader's config file to make sure the kext is enabled.
4. If you're using [VirtualSMC](https://github.com/acidanthera/VirtualSMC) you can also load SMCAMDProcessor.kext to publish sensor data.
5. Bootloaders like OpenCore will link each kext in the order they present in config file, so make sure AMDRyzenCPUPowerManagement.kext comes before SMCAMDProcessor.kext as it serves as a dependency.

### AMD Power Gadget
<img src="imgs/all.png" width="80%">


## Features
* CPU power management for AMD 17h processors. 
* Supports for reading of temperature, energy and frequency data on AMD 17h Processors.
* Manual switching of processor speed.
* PState editing.

## Passive Power Management
This options serves as a temporary solution to CPU power management due to no active solution are currently available. Comparing to a true active power managment implementation, this option works in a passive way which results in less sensitivity, accuracy and a slow down in performance.

I have been exploring possibilities for implementing a real active power management solution for AMD 17h platform. From what it looks like currently it is definitly possible. I will keep updating here with my latest progress.

<img src="imgs/ani.gif" width="100%">


## Editing PState

Since the release 0.3.1, you can now edit your CPU PState using AMD Power Tool.
<img src="imgs/pe.png" width="60%">

To access PState editor:
1. Open AMD Power Tool
2. Go to 'Speed' tab
3. Click 'Advanced Options'

#### Safety Notes
* Incorrect PState setting can potentially cause permanent damage to your computer hardware.
* For safety concern, this function was limited to root user only. You can either launch AMD Power Gadget with root user or use `-amdpnopchk` to disable this check.



## Tested Processors
* Ryzen 9 3900X
* Ryzen 7 3700X
* Ryzen 7 2700X
* Ryzen 5 3600
* Threadripper 2990WX

<img src="imgs/iStats.png" width="40%">


## Contribution
#### If you want to support this project, please:

* Give it a star! 😄
* Feel free to open up an issue if it works for you and not listed on supported processors.
* or if something breaks, please also open an issue.

* If you like to help with some coding, feel free to submit any pull request or just DM me on Discord.

## Credits
* [necross2](https://github.com/necross2) for adding support to temperature sensor offset.
* [Shaneee](https://github.com/Shaneee) for the beautiful icon.

## Notes
* I am still fairly new to macOS kernel development, this software project was initally a hobby project, **and it still is**, to get some reading on my newly built AMD hackintosh computer.

* With that being said, please bear with some of the spaghetti and not-idiomatic codes. Any criticism is much welcomed :)


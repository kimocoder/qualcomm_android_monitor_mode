
# qualcomm_android_monitor_mode
Qualcomm QCACLD WiFi (Android) monitor mode

[![Monitor mode](https://img.shields.io/badge/monitor%20mode-working-brightgreen.svg)](#)
[![GitHub version](https://raster.shields.io/badge/version-DEV-lightgrey.svg)](#)
[![GitHub issues](https://img.shields.io/github/issues/kimocoder/qualcomm_android_monitor_mode.svg)](https://github.com/kimocoder/qualcomm_android_monitor_mode/issues)
[![GitHub forks](https://img.shields.io/github/forks/kimocoder/qualcomm_android_monitor_mode.svg)](https://github.com/kimocoder/qualcomm_android_monitor_mode/network)
[![GitHub stars](https://img.shields.io/github/stars/kimocoder/qualcomm_android_monitor_mode.svg)](https://github.com/kimocoder/qualcomm_android_monitor_mode/stargazers)
[![Build Status](https://travis-ci.org/kimocoder/qualcomm_android_monitor_mode.svg?branch=master)](https://travis-ci.org/kimocoder/qualcomm_android_monitor_mode)
[![GitHub license](https://img.shields.io/github/license/kimocoder/qualcomm_android_monitor_mode.svg)](https://github.com/kimocoder/qualcomm_android_monitor_mode/blob/master/LICENSE)
<br>
[![Kali](https://img.shields.io/badge/Kali-supported-blue.svg)](https://www.kali.org)
[![Arch](https://img.shields.io/badge/Arch-supported-blue.svg)](https://www.archlinux.org)
[![Armbian](https://img.shields.io/badge/Armbian-supported-blue.svg)](https://www.armbian.com)
[![ArchLinux](https://img.shields.io/badge/ArchLinux-supported-blue.svg)](https://img.shields.io/badge/ArchLinux-supported-blue.svg)
[![aircrack-ng](https://img.shields.io/badge/aircrack--ng-supported-blue.svg)](https://github.com/aircrack-ng/aircrack-ng)
[![wifite2](https://img.shields.io/badge/wifite2-supported-blue.svg)](https://github.com/derv82/wifite2)


### NOTES
```
  Monitor mode on QCACLD (QualComm) WiFi (Android) driver is very much possible as the
  modes has been supported all the way, but I stumbled upon a switch that Qualcomm/vendors had DISABLED.
  
  We've added some screenshots / tests of 'airodump-ng', 'wifite' and 'tcpdump' down at the bottom here.
```

### DEPENDENCIES
```
  1. A rooted Android environment.
  2. Either compile a kernel yourself (NetHunter chroot works)
  3. WiFi chipset that actually uses the QCACLD driver/firmware.
  
  Older devices/drivers would need the patch from 'files', future kernels of 4.9, 4.14, 4.19
  may have it WORKING from vendor. I see most wan't it turned OFF, some not .. We'll see!
```


### HowTo GeT it MONITORING !

Configure device to deliver 802.11 packets in raw mode.
Below is the example of starting monitor mode and channel settings + tcpdump

```sh
$ insmod /system/lib/modules/wlan.ko con_mode=4
$ ifconfig wlan0 up
$ "iwpriv wlan0 setMonChan 36 2"

or

$ iw dev mon0 set channel 36 HT40+
$ tcpdump -i wlan0 -w <tcpdump.pcap>
```


<br><br><br>
### Logs / Outputs
```
* 'iw phy0 info' output is over [here](https://github.com/kimocoder/qualcomm_android_monitor_mode/blob/master/docs/iwphy_output.txt)
```

<br><br><br>
### Credits
* kimocoder
  * Twitter: https://twitter.com/kimocoder
  * Telegram channel: https://t.me/joinchat/AAAAAFDVPDIHabBJwhL1Mw

* Qualcomm
  * https://www.qualcomm.com

* CodeAurora
  * https://www.codeaurora.org
<br><br><br>


### Downloads / Patches
  * Android QCACLD-3.0 patch to enable monitor mode - [DOWNLOAD HERE](https://github.com/kimocoder/qualcomm_android_monitor_mode/raw/master/files/enable_monitor_mode.patch)

<br><br><br>
#### Here are some tests done by @re4son and @DJY below..
#### Seems to be working just about perfect.
<br><br>
![Setting up a custom command](https://i.imgur.com/cTJhOTB.jpg)
<br><br>
![Running monitor mode](https://i.imgur.com/s5gzFso.jpg)
<br><br>
![Running wifite2](https://i.imgur.com/VNpiXEk.jpg)
<br><br><br><br><br><br>


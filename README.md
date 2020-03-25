
# qualcomm_android_monitor_mode
Qualcomm QCACLD WiFi (Android) monitor mode

[![Monitor mode](https://img.shields.io/badge/monitor%20mode-working-brightgreen.svg)](#)
[![GitHub version](https://raster.shields.io/badge/version-DEV-lightgrey.svg)](#)
[![GitHub issues](https://img.shields.io/github/issues/kimocoder/qualcomm_android_monitor_mode.svg)](https://github.com/aircrack-ng/rtl8812au/issues)
[![GitHub forks](https://img.shields.io/github/forks/kimocoder/qualcomm_android_monitor_mode.svg)](https://github.com/aircrack-ng/rtl8812au/network)
[![GitHub stars](https://img.shields.io/github/stars/kimocoder/qualcomm_android_monitor_mode.svg)](https://github.com/aircrack-ng/rtl8812au/stargazers)
[![Build Status](https://travis-ci.org/kimocoder/qualcomm_android_monitor_mode.svg?branch=master)](https://travis-ci.org/aircrack-ng/rtl8812au)
[![GitHub license](https://img.shields.io/github/license/kimocoder/qualcomm_android_monitor_mode.svg)](https://github.com/aircrack-ng/rtl8812au/blob/master/LICENSE)
<br>
[![Kali](https://img.shields.io/badge/Kali-supported-blue.svg)](https://www.kali.org)
[![Arch](https://img.shields.io/badge/Arch-supported-blue.svg)](https://www.archlinux.org)
[![Armbian](https://img.shields.io/badge/Armbian-supported-blue.svg)](https://www.armbian.com)
[![ArchLinux](https://img.shields.io/badge/ArchLinux-supported-blue.svg)](https://img.shields.io/badge/ArchLinux-supported-blue.svg)
[![aircrack-ng](https://img.shields.io/badge/aircrack--ng-supported-blue.svg)](https://github.com/aircrack-ng/aircrack-ng)
[![wifite2](https://img.shields.io/badge/wifite2-supported-blue.svg)](https://github.com/derv82/wifite2)


### DEPENDENCIES
```
  * A rooted Android environment.
  * A custom kernel (for now, as the firmware needs patch)
    - defconfig will need to have "CONFIG_WIRELESS_EXT" and "CONFIG_WEXT" enabled

  * WiFi chipset that uses the QCACLD driver/firmware.
```


### Where did you find it?!
I was fiddling around with IOCTL/monitor mode on another project,
and ended up finding this commit https://github.com/MotorolaMobilityLLC/vendor-qcom-opensource-wlan-qcacld-3.0/commit/59f861d11d0daf043e33b23f2e3a050453ca6cb0

The howto is seen in the commit above
```
Configure target to deliver 802.11 packets
in raw mode. Below is the procedure to start the monitor mode.

$ insmod /system/lib/modules/wlan.ko con_mode=4
$ ifconfig wlan0 up
$ "iwpriv wlan0 setMonChan 36 2"
or
$ "iw dev mon0 set channel 36 HT40+"
$ tcpdump -i wlan0 -w <tcpdump.pcap>
```

And from there I got interested right away, as QCACLD is used in various devices.

Second I've found the parameter
"con_mode_monitor" in the commit here https://gitlab.com/Codeaurora/platform_vendor_qcom-opensource_wlan_qcacld-3.0/-/commit/a307f63059c7fb5e89c12e057d80fe0948c11e3b

However, the option is nowhere to be find in the list
```
$ iwpriv wlan0 | grep "con_mode"
```
Revealed it's not there.. So where else may I see the string/alias?
```
$ 
```

The image below explains it all, all code is present,
but monitor mode is turned off by default.


[IMAGE IS COMING]






### Credits
* kimocoder
  Twitter: https://twitter.com/kimocoder
  Telegram channel: https://t.me/joinchat/AAAAAFDVPDIHabBJwhL1Mw

* Qualcomm

* CodeAurora



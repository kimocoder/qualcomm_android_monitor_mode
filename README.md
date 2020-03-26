
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


### FIRST OFF!
```
  * This script/mod is EXPERIMENTAL as it is a development project and
    must be used with CAUTION. YOUR ON YOUR OWN [ IF BRICKED ] OR SO !!
```

### TODO
```
  * Finish up the WRITE-UP
  * Add PDF papers (datasheet) or/any docs related
  * Upload missing images attached to above
  * Add a proper SETUP / HELP section
  * Add a list of devices supported
  * Clean up the README.md
```


### DEPENDENCIES
```
  * A rooted Android environment.
  * A custom kernel (for now, as the firmware needs patch)
    - defconfig will need to have "CONFIG_WIRELESS_EXT" and "CONFIG_WEXT" enabled

  * WiFi chipset that uses the QCACLD driver/firmware.
```


### Logs / Outputs
  * 'iw phy0 info' output is over [here](https://github.com/kimocoder/qualcomm_android_monitor_mode/blob/master/docs/iwphy_output.txt)



### Where did you find it?!
I was fiddling around with IOCTL/monitor mode on another project,
and ended up finding this commit [here](https://github.com/MotorolaMobilityLLC/vendor-qcom-opensource-wlan-qcacld-3.0/commit/59f861d11d0daf043e33b23f2e3a050453ca6cb0)

The howto is seen in the commit above
```sh
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
"con_mode_monitor" in the commit [here](https://gitlab.com/Codeaurora/platform_vendor_qcom-opensource_wlan_qcacld-3.0/-/commit/a307f63059c7fb5e89c12e057d80fe0948c11e3b)

However, the option is nowhere to be find in the list
```sh
$ ip link set wlan0 up
$ iwpriv wlan0

wlan0     Available private ioctls :
          set11Dstate      (0001) : set   1 int   & get   0      
          wowl             (0002) : set   1 int   & get   0      
          setPower         (0003) : set   1 int   & get   0      
          setMaxAssoc      (0004) : set   1 int   & get   0      
          scan_disable     (0005) : set   1 int   & get   0      
          inactivityTO     (0006) : set   1 int   & get   0      
          wow_ito          (005E) : set   1 int   & get   0      
          setMaxTxPower    (0007) : set   1 int   & get   0      
          setTxPower       (004A) : set   1 int   & get   0      
          setMcRate        (0051) : set   1 int   & get   0      
          setTxMaxPower2G  (002A) : set   1 int   & get   0      
          setTxMaxPower5G  (002B) : set   1 int   & get   0      
          setTxMaxPower    (0007) : set   1 int   & get   0      
          setTmLevel       (0009) : set   1 int   & get   0      
          setphymode       (000A) : set   1 int   & get   0      
          nss              (000B) : set   1 int   & get   0      
          ldpc             (000C) : set   1 int   & get   0      
          tx_stbc          (000D) : set   1 int   & get   0      
          rx_stbc          (000E) : set   1 int   & get   0      
          shortgi          (000F) : set   1 int   & get   0      
          enablertscts     (0010) : set   1 int   & get   0      
          chwidth          (0011) : set   1 int   & get   0      
          anienable        (0012) : set   1 int   & get   0      
          aniplen          (0013) : set   1 int   & get   0      
          anilislen        (0014) : set   1 int   & get   0      
          aniofdmlvl       (0015) : set   1 int   & get   0      
          aniccklvl        (0016) : set   1 int   & get   0      
          cwmenable        (0017) : set   1 int   & get   0      
          cts_cbw          (0054) : set   1 int   & get   0      
          gtxHTMcs         (003E) : set   1 int   & get   0      
          gtxVHTMcs        (003F) : set   1 int   & get   0      
          gtxUsrCfg        (0040) : set   1 int   & get   0      
          gtxThre          (0041) : set   1 int   & get   0      
          gtxMargin        (0042) : set   1 int   & get   0      
          gtxStep          (0043) : set   1 int   & get   0      
          gtxMinTpc        (0044) : set   1 int   & get   0      
          gtxBWMask        (0045) : set   1 int   & get   0      
          txchainmask      (0018) : set   1 int   & get   0      
          rxchainmask      (0019) : set   1 int   & get   0      
          set11NRates      (001A) : set   1 int   & get   0      
          set11ACRates     (0027) : set   1 int   & get   0      
          ampdu            (001B) : set   1 int   & get   0      
          amsdu            (001C) : set   1 int   & get   0      
          txpow2g          (001D) : set   1 int   & get   0      
          txpow5g          (001E) : set   1 int   & get   0      
          txrx_fw_stats    (0026) : set   1 int   & get   0      
          txrx_stats       (005A) : set   2 int   & get   0      
          txrx_fw_st_rst   (0029) : set   1 int   & get   0      
          paid_match       (002D) : set   1 int   & get   0      
          gid_match        (002E) : set   1 int   & get   0      
          tim_clear        (002F) : set   1 int   & get   0      
          dtim_clear       (0030) : set   1 int   & get   0      
          eof_delim        (0031) : set   1 int   & get   0      
          mac_match        (0032) : set   1 int   & get   0      
          delim_fail       (0033) : set   1 int   & get   0      
          nsts_zero        (0034) : set   1 int   & get   0      
          rssi_chk         (0035) : set   1 int   & get   0      
          5g_ebt           (0053) : set   1 int   & get   0      
          htsmps           (0037) : set   1 int   & get   0      
          set_qpspollcnt   (0038) : set   1 int   & get   0      
          set_qtxwake      (0039) : set   1 int   & get   0      
          set_qwakeintv    (003A) : set   1 int   & get   0      
          set_qnodatapoll  (003B) : set   1 int   & get   0      
          setMccLatency    (0046) : set   1 int   & get   0      
          setMccQuota      (0047) : set   1 int   & get   0      
          setDbgLvl        (0048) : set   1 int   & get   0      
          erx_enable       (004B) : set   1 int   & get   0      
          erx_bmiss_val    (004C) : set   1 int   & get   0      
          erx_bmiss_smpl   (004D) : set   1 int   & get   0      
          erx_slop_step    (004E) : set   1 int   & get   0      
          erx_init_slop    (004F) : set   1 int   & get   0      
          erx_adj_pause    (0050) : set   1 int   & get   0      
          erx_dri_sample   (0052) : set   1 int   & get   0      
          dumpStats        (0055) : set   1 int   & get   0      
          clearStats       (0056) : set   1 int   & get   0      
          startProfile     (0057) : set   1 int   & get   0      
          setChanChange    (0058) : set   1 int   & get   0      
          setConcSysPref   (0059) : set   1 int   & get   0      
          pdev_reset       (005F) : set   1 int   & get   0      
          setModDTIM       (0060) : set   1 int   & get   0      
          get11Dstate      (0001) : set   0       & get   1 int  
          getwlandbg       (0004) : set   0       & get   1 int  
          getMaxAssoc      (0006) : set   0       & get   1 int  
          getAutoChannel   (0008) : set   0       & get   1 int  
          getconcurrency   (0009) : set   0       & get   1 int  
          get_nss          (000B) : set   0       & get   1 int  
          get_ldpc         (000C) : set   0       & get   1 int  
          get_tx_stbc      (000D) : set   0       & get   1 int  
          get_rx_stbc      (000E) : set   0       & get   1 int  
          get_shortgi      (000F) : set   0       & get   1 int  
          get_rtscts       (0010) : set   0       & get   1 int  
          get_chwidth      (0011) : set   0       & get   1 int  
          get_anienable    (0012) : set   0       & get   1 int  
          get_aniplen      (0013) : set   0       & get   1 int  
          get_anilislen    (0014) : set   0       & get   1 int  
          get_aniofdmlvl   (0015) : set   0       & get   1 int  
          get_aniccklvl    (0016) : set   0       & get   1 int  
          get_cwmenable    (0017) : set   0       & get   1 int  
          get_gtxHTMcs     (002F) : set   0       & get   1 int  
          get_gtxVHTMcs    (0030) : set   0       & get   1 int  
          get_gtxUsrCfg    (0031) : set   0       & get   1 int  
          get_gtxThre      (0032) : set   0       & get   1 int  
          get_gtxMargin    (0033) : set   0       & get   1 int  
          get_gtxStep      (0034) : set   0       & get   1 int  
          get_gtxMinTpc    (0035) : set   0       & get   1 int  
          get_gtxBWMask    (0036) : set   0       & get   1 int  
          get_txchainmask  (0018) : set   0       & get   1 int  
          get_rxchainmask  (0019) : set   0       & get   1 int  
          get_11nrate      (001A) : set   0       & get   1 int  
          get_ampdu        (001B) : set   0       & get   1 int  
          get_amsdu        (001C) : set   0       & get   1 int  
          get_txpow2g      (001D) : set   0       & get   1 int  
          get_txpow5g      (001E) : set   0       & get   1 int  
          get_paid_match   (0020) : set   0       & get   1 int  
          get_gid_match    (0021) : set   0       & get   1 int  
          get_tim_clear    (0022) : set   0       & get   1 int  
          get_dtim_clear   (0023) : set   0       & get   1 int  
          get_eof_delim    (0024) : set   0       & get   1 int  
          get_mac_match    (0025) : set   0       & get   1 int  
          get_delim_fail   (0026) : set   0       & get   1 int  
          get_nsts_zero    (0027) : set   0       & get   1 int  
          get_rssi_chk     (0028) : set   0       & get   1 int  
          get_qpspollcnt   (0029) : set   0       & get   1 int  
          get_qtxwake      (002A) : set   0       & get   1 int  
          get_qwakeintv    (002B) : set   0       & get   1 int  
          get_qnodatapoll  (002C) : set   0       & get   1 int  
          cap_tsf          (003A) : set   0       & get   1 int  
          get_temp         (0038) : set   0       & get   1 int  
          get_dcm          (003C) : set   0       & get   1 int  
          get_range_ext    (003D) : set   0       & get   1 int  
          wowlAddPtrn      (0001) : set 512 char  & get   0      
          wowlDelPtrn      (0002) : set 512 char  & get   0      
          neighbor         (0003) : set 512 char  & get   0      
          set_ap_wps_ie    (0004) : set 512 char  & get   0      
          setConfig        (0005) : set 512 char  & get   0      
          setwlandbg       (0001) : set   3 int   & get   0      
          fw_test          (0004) : set   3 int   & get   0      
          get_tsf          (0001) : set   0       & get   3 int  
          set_scan_cfg     (0015) : set   3 int   & get   0      
          version          (0001) : set   0       & get 2047 char 
          getStats         (0002) : set   0       & get 2047 char 
          getSuspendStats  (0007) : set   0       & get 2047 char 
          listProfile      (000F) : set   0       & get 2047 char 
          getHostStates    (000A) : set   0       & get 2047 char 
          getConfig        (0003) : set   0       & get 2047 char 
          getRSSI          (0006) : set   0       & get 2047 char 
          getWmmStatus     (0004) : set   0       & get 2047 char 
          getChannelList   (0005) : set   0       & get 2047 char 
          getTdlsPeers     (0008) : set   0       & get 2047 char 
          getPMFInfo       (0009) : set   0       & get 2047 char 
          getIbssSTAs      (000B) : set   0       & get 2047 char 
          getphymode       (000C) : set   0       & get 2047 char 
          getOemDataCap    (000D) : set   0       & get 2047 char 
          getSNR           (000E) : set   0       & get 2047 char 
          ibssPeerInfoAll  (000A) : set   0       & get   0      
          getRecoverStat   (0011) : set   0       & get   0      
          getProfileData   (0012) : set   0       & get   0      
          reassoc          (0008) : set   0       & get   0      
          stop_obss_scan   (0013) : set   0       & get   0      
          ibssPeerInfo     (0006) : set  11 int   & get   0      
          pm_cinfo         (000F) : set  11 int   & get   0      
          setUnitTestCmd   (0007) : set  11 int   & get   0      
          halPwrDebug      (0004) : set  11 int   & get   0      
          fips_test        (8BE8) : set 2047 byte  & get 2047 byte 
          addTspec         (8BE9) : set  19 int   & get   1 int  
          delTspec         (8BEB) : set   1 int   & get   1 int  
          getTspec         (8BED) : set   1 int   & get   1 int  
          setHostOffload   (8BF2) : set  24 byte  & get   0      
          getWlanStats     (8BF5) : set   0       & get 2047 byte 
          setKeepAlive     (8BF6) : set  32 byte  & get   0      
          setPktFilter     (8BF7) : set 103 byte  & get   0      
          setpno           (8BF8) : set 2047 char  & get   0      
          SETBAND          (8BF9) : set   1 int   & get   0      
          setMCBCFilter    (8BFA) : set   0       & get   0      
          getLinkSpeed     (8BFF) : set  18 char  & get   5 char 
          set_smps_param   (0001) : set   2 int   & get   0      
          set_dot11p       (8BFE) : set 208 byte  & get   0      
          log_buffer       (0008) : set   2 int   & get   0      
          enableProfile    (0004) : set   2 int   & get   0      
          set_hist_intvl   (0005) : set   2 int   & get   0      
          set_fw_mode_cfg  (0016) : set   2 int   & get   0      
          hostroamdelay    (003B) : set   0       & get   1 int  
          set_11ax_rate    (005B) : set   1 int   & get   0      
          enable_dcm       (005C) : set   1 int   & get   0      
          range_ext        (005D) : set   1 int   & get   0      
          set_ft_ies       (8BF4) : set 384 char  & get   0      
```
Revealed it's not there.. So where else may I see the string/alias?
```sh
$ tba
```

### Downloads / Patches
  * Android QCACLD-3.0 patch to enable monitor mode - [DOWNLOAD HERE](https://github.com/kimocoder/qualcomm_android_monitor_mode/raw/master/files/enable_monitor_mode.patch)

<br><br><br>
![Switch added around the monitor mode alias/string](https://i.imgur.com/zD1br4j.jpg)
<br><br>
![Info](https://i.imgur.com/zp1zfqv.jpg)
<br><br>
![Found a script present on the system](https://i.imgur.com/t1wBlun.jpg)



The image below explains it all, all code is present,
but monitor mode is turned off by default.


[IMAGES IS COMING]






### Credits
* kimocoder
  * Twitter: https://twitter.com/kimocoder
  * Telegram channel: https://t.me/joinchat/AAAAAFDVPDIHabBJwhL1Mw

* Qualcomm
  * https://www.qualcomm.com

* CodeAurora
  * https://www.codeaurora.org


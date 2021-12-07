# Hackintosh on Dell Precision 3240 Compact PC (OpenCore) Comet-lake

## What works

* OpenCore (0.7.6)
* Supported OS
    * macOS Monterey (12.0)
    * macOS Big Sur (11.4)
    * macOS Catalina (10.15)
* All USB Ports at full speed (USB 3.2) (via Custom USB Mapping)
* Intel UHD Graphics 630 - 4K UHD @ 60hz (Displayport)
* Full Metal hardware acceleration
* Sleep, wake and power nap
* Audio - Internal Speaker and front audio port
* Airplay, Sidecard, Continuity, Airdrop, Facetime, iMessage and Handoff - If you have the right Wifi card (tested with BCM94360NG M.2 Wifi Card)

## Changelog

### 2021-12-07
* Upgraded to OpenCore 0.7.6
* Updated kexts

### 2021-11-22
* Upgraded to OpenCore 0.7.5
* Removed `CPUFriendDataProvider` as it was causing issues with CPU fan speeds and also wake-up time.  It is also recommended to install a fan control app (eg. [smcFanControl](https://github.com/hholtmann/smcFanControl)) and increase to max to help decrease temps.
* Added `AirportBrcmFixup.kext` which seemed to fix some bluetooth issues (eg. slow cursor with magic mouse)

### 2021-09-25
* Updated to OpenCore 0.7.4 (2021-09-23)
* Dell BIOS 1.16.0
* Removed `FakePCIID.kext` and `FakePCIID_Intel_HDMI_Audio.kext` (HDMI audio no longer required)

## Installation

* Mount EFI Partition
* Copy `EFI` folder to EFI Partition root `(/)`
* Replace the following values in `EFI/OC/config.plist` with generated values from [GenSMBios](https://github.com/corpnewt/GenSMBIOS)
    * PlatformInfo --> Generic --> SystemSerialNumber
    * PlatformInfo --> Generic --> MLB
    * PlatformInfo --> Generic --> SystemUUID

## Bios Settings

Tested with BIOS version 1.16.0

Update the following settings in BIOS with [RU.exe](http://ruexe.blogspot.com/) or [bios-extraction-guide (Dell)](https://github.com/dreamwhite/bios-extraction-guide/tree/master/Dell)

| UEFI Variable | Offset | Value | Comment       |
| ------------- | ------ | ----- | ------------- |
| SaSetup       | 0xF5   | 0x2   | DVMT: 64M     |
| CpuSetup      | 0x3E   | 0x0   | CFG Lock: OFF |


Update the following settings in BIOS:

| Item              | Value             |
| ----------------- | ----------------- |
| **System Configuration** |
| Memory Map IO above 4GB | Enabled |
| **Security** |
| TPM 2.0 Security               | Disabled          |
| **Secure Boot** |
| Secure Boot Enable       | Disabled          |
| **Intel Software Guard Extensions** |
| Intel SGX Enable         | Disabled          |
| **Performance** |
| Intel SpeedStep | Enabled |
| C-States Control | Enabled | 
| Cache Prefetch | Hardware Prefetched - Enabled |
| | Adjacent Cache Prefetcher - Enabled |
| Intel Turbo Boost | Enabled |
| HyperThread Control | Enabled |
| Enable Intel Speed Shift Technology | Enabled |
| **Power Management** |
| Deep Sleep Control | Enabled in S4 and S5 |
| USB Wake Support | Disabled |
| **Virtualization** |
| Virtualization | Enabled |
| VT for Direct I/O | Enabled          |


## Post Install

### Power management Settings

Disable hibernation, act like a real mac

```
sudo pmset standby 0
sudo pmset autopoweroff 0 
sudo pmset proximitywake 0
sudo pmset powernap 0 
sudo pmset tcpkeepalive 0
sudo pmset womp 0
sudo pmset hibernatemode 0
```

Delete the sleepimage file and block MacOS from creating it again.

```
sudo rm /var/vm/sleepimage
sudo mkdir /var/vm/sleepimage
```


## Credits

* https://github.com/billzhong/dell-precision-3240-compact-hackintosh
* https://github.com/zearp/Nucintosh


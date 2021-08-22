# Hackintosh on Dell Precision 3240 Compact PC (OpenCore) Comet-lake

<<<<<<< HEAD
## What works

* OpenCore (0.7.0)
* Supported OS
    * macOS Big Sur (11.4)
    * macOS Catalina (10.15)
* All USB Ports at full speed (USB 3.2) (via Custom USB Mapping)
* Intel UHD Graphics 630 - 4K UHD @ 60hz (Displayport)
* CPU Low Frequency mode set to `800Mhz` (via `CPUFriendDataProvider`) 
* Full Metal hardware acceleration
* Sleep, wake and power nap
* Audio - Internal Speaker, Displayport/HDMI, and front audio port
* Airplay, Sidecard, Continuity, Airdrop, Facetime, iMessage and Handoff - If you have the right Wifi card (tested with BCM94360NG M.2 Wifi Card)

## What's not working

Nothing!
=======
Originally forked from [dell-precision-3240-compact-hackintosh](https://github.com/billzhong/dell-precision-3240-compact-hackintosh/) and modified with my own preferred settings.
>>>>>>> 03ae924 (OC 0.7.2)

## Installation

* Mount EFI Partition
* Copy `EFI` folder to EFI Partition root `(/)`
* Replace the following values in `EFI/OC/config.plist` with generated values from [GenSMBios](https://github.com/corpnewt/GenSMBIOS)
    * PlatformInfo --> Generic --> SystemSerialNumber
    * PlatformInfo --> Generic --> MLB
    * PlatformInfo --> Generic --> SystemUUID

## Bios Settings

Update the following settings in BIOS with [RU.exe](http://ruexe.blogspot.com/) or [bios-extraction-guide (Dell)](https://github.com/dreamwhite/bios-extraction-guide/tree/master/Dell)

| UEFI Variable | Offset | Value | Comment       |
| ------------- | ------ | ----- | ------------- |
| SaSetup       | 0xF5   | 0x2   | DVMT: 64M     |
| CpuSetup      | 0x3E   | 0x0   | CFG Lock: OFF |


Update the following settings in BIOS:

| Item              | Value             |
| ----------------- | ----------------- |
| Intergrated NIC   | Enabled           |
| SATA Operation    | AHCI              |
| Primary Display   | Intel HD Graphics |
| TPM               | Disabled          |
| Secure Boot       | Disabled          |
| Intel SGX         | Disabled          |
| VT for Direct I/O | Disabled          |



## What works

* OpenCore (0.7.2)
* Supported OS
    * macOS Big Sur (11.5.2)
    * macOS Catalina (10.15)
* All USB Ports at full speed (USB 3.2) (via Custom USB Mapping)
* Intel UHD Graphics 630 - 4K UHD @ 60hz (Displayport)
* Full Metal hardware acceleration
* Sleep, wake and power nap
* Audio - Internal Speaker, Displayport/HDMI, and front audio port
* Airplay, Sidecard, Continuity, Airdrop, Facetime, iMessage and Handoff - If you have the right Wifi card (tested with BCM94360NG M.2 Wifi Card)

## What doesn't work

* Displayport audio stops working (disappears from Sound devices) after waking up from sleep

## Tested Configuration

| Component | Tested                             |
| --------- | ---------------------------------- |
| CPU       | Core i5 10500                      |
| Chipset   | Intel W480                         |
| Graphics  | Intel UHD 630                      |
| Ethernet  | Intel I219-LM                      |
| NVME      | WD SN550 (2)                       |
| HDD       | ST2000LM007 (Fusion drive)         |
| Memory    | Crucial 32GB Kit (16GB x 2) DDR4 3200 MT/s (PC4-25600) |
| Sound     | ALC3246 (ALC256)                   |
| Wireless  | BCM94360NG                         |


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


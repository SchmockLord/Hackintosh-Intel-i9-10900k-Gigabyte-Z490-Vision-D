# Hackintosh-Intel-i9-10900k-Gigabyte-Z490-Vision-D

**This guide it's updated to OpenCore 0.7.2 and tested on my main device.**
<!-- shields -->
<div>
    <!-- downloads -->
    <a href="https://github.com/RobyRew/GIGABYTE-Z490-Vision-D_i9-10900K_Hackintosh/releases">
        <img src="https://img.shields.io/github/downloads/RobyRew/GIGABYTE-Z490-Vision-D_i9-10900K_Hackintosh/total" alt="downloads"/>
    </a>
    <!-- version -->
    <a href="https://github.com/RobyRew/GIGABYTE-Z490-Vision-D_i9-10900K_Hackintosh/releases/latest">
        <img src="https://img.shields.io/github/release/RobyRew/GIGABYTE-Z490-Vision-D_i9-10900K_Hackintosh.svg" alt="latest version"/>
    </a>
    <!-- platform -->
    <a href="https://github.com/RobyRew/GIGABYTE-Z490-Vision-D_i9-10900K_Hackintosh">
        <img src="https://img.shields.io/badge/platform-macOS-lightgrey.svg" alt="platform"/>
    </a>
</div>
</br></br>

![MyPC running macOS Big Sur](/Docs/Images/NZXT_PC-macOS.png)


## Specs:
| Component | Name |
|:--- |:---:|
| Motherboard:  | FX504GE **HM370** |
| CPU: | Intel i9 10900K |
| RAM: | 16GB **SK Hyinix** HMA82GS6CJR8N-VK 2666Mhz |
| iGPU: | Intel UHD 630 (Mobile) |
| dGPU: | NVIDIA GeForce GTX 1050 Ti (DISABLED) |
| NVMe: | Samsung 970 EVO Plus |
| HDD: | HGST HTS721010A9E630 |
| Wifi/BT: | Intel(R) Wireless-AC 9560 160MHz (Type CNVi) |
| Audio: | RealTek ALC255 |
| Ethernet: | Realtek RTL8111 |
| Trackpad: | ELAN1200 Precision TouchPad (Type HID) |
| Keyboard: | Standard PS/2 Keyboard |

![Asus FX504GE Layout](/Docs/Images/Guide/NZXT_PC-macOS-layout.png)
These are all the external ports of the laptop. (**They all work**)

### Working
- [x] **Tested with macOS High Sierra, Mojave, Catalina, Big Sur, and Monterrey**
- [x] **Wifi** (Thanks to [AirportItlwm.kext](https://github.com/OpenIntelWireless/itlwm/releases) and loading from system the kext: `IO80211Family.kext`)
- [x] **Bluetooth:** (Thanks to [IntelBluetoothFirmware.kext](https://github.com/OpenIntelWireless/IntelBluetoothFirmware/releases))
- [x] **Audio:** Realtek ALC255 (Thanks to AppleALC.kext with layout-id=3 setted in Device Properties)
- [x] **USB:** All internal and external ports (Thanks to SSDT-EC-USBX-LAPTOP.aml)
- [x] **Ethernet:** Realtek RTL8111 (Thanks to RealtekRTL8111.kext)
- [x] **Trackpad:** (Working thanks to VoodooI2C.kext, VoodooI2CHID.kext and SSDT-XOSI.aml)
- [x] **HDMI:** Works almost perfect. 
- [x] **Shutdown:** Yes
- [x] **Restart:** Yes
- [x] **Sleep/Wake:** Yes

### Not working
- dGPU (Any support in Mojave and up).
- Continuity Features (not working for now, waiting on https://openintelwireless.github.io/).


```bash
```

# INSTALLATION GUIDE

---

## Making the Booteable USB

### From macOS:
[**Link to Apple's Guide**](https://support.apple.com/en-us/HT201372)

**Download installers:** [Monterrey Beta 5](http://swcdn.apple.com/content/downloads/45/34/071-79810-A_PHL4H4X2JM/6mnb23uh2somxqw1jkxm2mos6op8qjcij8/InstallAssistant.pkg)(Execute de .pkg to extract the installer) - [Big Sur](https://itunes.apple.com/us/app/macos-big-sur/id1526878132) - [Catalina](https://itunes.apple.com/us/app/macos-catalina/id1466841314) - [Mojave](https://itunes.apple.com/us/app/macos-mojave/id1398502828) - [High Sierra](https://itunes.apple.com/us/app/macos-high-sierra/id1246284741)

1. Connect a >=16 GB pendrive.
2. Open *Disk Utility* and Erase the USB with the name: *MyVolume*.
3. Open *Terminal* and use the proper commands for your macOS installer:
- Monterrey: `sudo /Applications/Install\ macOS\ 12\ Beta.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume`
- Big Sur: `sudo /Applications/Install\ macOS\ Big\ Sur.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume`
- Catalina: `sudo /Applications/Install\ macOS\ Catalina.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume`
- Mojave: `sudo /Applications/Install\ macOS\ Mojave.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume`
- High Sierra: `sudo /Applications/Install\ macOS\ High\ Sierra.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume`

![Terminal](/Docs/Images/Guide/BootableUSB.png)

### From Windows:

[**Link to Dortania's Guide**](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/winblows-install.html)

### From Linux:

[**Link to Dortania's Guide**](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/linux-install.html)


---

# BIOS Settings:
- Make Sure you have [Latest BIOS vF20](https://download.gigabyte.com/FileList/BIOS/mb_bios_z490-vision-d_f20.zip)
- After Updating the BIOS, stock configuration works, so don't worry about this part.

---

# OpenCore Configuration

## [Here it's my config.plist and the explanation:](/Docs/config.plist.md)
#### [ACPI](/Docs/config.plist.md#acpi)
#### [Booter](/Docs/config.plist.md#booter)
#### [DeviceProperties](/Docs/config.plist.md#deviceproperties)
#### [Kernel](/Docs/config.plist.md#kernel)
#### [Misc](/Docs/config.plist.md#misc)
#### [NVRAM](/Docs/config.plist.md#nvram)
#### [PlatformInfo](/Docs/config.plist.md#platforminfo)
#### [UEFI](/Docs/config.plist.md#uefi)

---

# Post Install (Important!!)
Open Terminal.app and run those commands:
```bash
sudo rm /Library/Preferences/SystemConfiguration/NetworkInterfaces.plist
sudo rm /Library/Preferences/SystemConfiguration/preferences.plist
```
---

# BenchMarks:
#### Cinebench R23:
![Cinebench R23](/Docs/Images/Benchmarks/Cinebench_R23.png)

#### GeekBench 5:
![GeekBench 5_CPU Score](/Docs/Images/Benchmarks/GeekBench5_CPU.png)
![GeekBench 5_GPU Score](/Docs/Images/Benchmarks/GeekBench5_GPU.png)
https://browser.geekbench.com/v5/cpu/

---

# Credits

[Apple](https://apple.com) (macOS)

[OpenCore Team](https://github.com/acidanthera/OpenCorePkg) (Bootloader)

[Dortania](https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/coffee-lake.html#starting-point) (Guide)

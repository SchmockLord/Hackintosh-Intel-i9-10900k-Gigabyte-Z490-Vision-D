# Hackintosh-Intel-i9-10900k-Gigabyte-Z490-Vision-D

Hello folks,

I have successfully installed MacOS Catalina 10.15.4 on my i9-10900k running on a Gigabyte Z490 Vision D.

You can find my EFI folder in this repository.

I will update this Build in the next days. The Build is very fresh (3h after the first successfull installation).

SMBIOS=MacBookAir9,1

OpenCore 0.5.8

# Hardware
- Intel i9 10900k
- Gigabyte Z490 Vision D
- Radeon VII
- 32GB 

# Working
- [x] Wifi and Bluetooth (via BCM94360CD using a MQUPIN fenvi T919 Wireless Card)
- [x] Audio: Realtek ALC1220-VB (AppleALC.kext, layout-id=7, device-id=0xA170, FakeID.kext, FakePCIID_Intel_HDMI_Audio.kext)
- [x] USB, all ports except the USB 2.0 on the rear panel labeled "BIOS". Disabled this due to the 15 port limit.
- [x] Thunderbolt 3 including Hot-plug
- [x] 1Gbit Ethernet (Intel I219-V)
- [x] Sleep/Wake
- [x] Shutdown
- [x] Restart

# Not working so far
- [ ] 2.5Gbit Ethernet (Intel I225-V)

# Details

## Audio

I needed this to get Audio working:
- AppleALC.kext
- FakeID.kext
- FakePCIID_Intel_HDMI_Audio.kext
- layout-id=7 
- device-id=0xA170

The layout-id and the device-id is injected via the device properties.

The audio device has the PCI-Address PciRoot(0x0)/Pci(0x1F,0x3).
```
<key>DeviceProperties</key>
	<dict>
		<key>Add</key>
		<dict>
			<key>PciRoot(0x0)/Pci(0x1F,0x3)</key>
			<dict>
				<key>device-id</key>
				<data>cKEAAA==</data>
				<key>layout-id</key>
				<data>BwAAAA==</data>
			</dict>
		</dict>
	</dict>
```

## Thunderbolt 3 Support

In your BIOS set the following settings:

Settings/IO-ports/Thunderbolt Configuration
Discrete Thunderbolt support: Enabled

then
GPIO3 Force Pwr: Enabled
Wait time in ms after applying Force Pwr: 200
GPIO filter: Enabled
Enable CLK REQ: Enabled
Enable ASPM: Disabled
Enable LTR: Disabled
Enable PTM: Disabled
Enable TBT ASPM L1.1 & L1.2

You also need the SSDT-TB3.aml in EFI/OC/ACPI to enable Thunerbolt Hotplug support.

## 1Gbit Ethernet (Intel I219-V)

Simply add the newest IntelMausiEthernet.kext (mine is v2.5.1d1).

## USB

I use USBInjectAll.kext and created my own SSDT-EC-USBX.aml and SSDT-UIAC.aml using Hackintool 3.4.0.

All ports are enabled, except for the USB 2.0 port that is labeled "BIOS" and intended to be used to flash the BIOS. I had to disable this to stay within the 15 port USB limit. And I don't need this port as much as the faster ones. BIOS flashing will work anyways, because this is done prior the Bootloader config.

## Wifi/Bluetooth
You need natively supported Wifi and Bluetooth to use Airdrop, Unlock with Apple Watch etc.

I used the MQUPIN fenvi T919 Wireless/Bluetooth Card. It has the natively supported WiFi and Bluetooth chip BCM94360CD. 

No further kexts needed (no AirportBrcmFixup.kext, BrcmBluetoothInjector.kext, BrcmFirmwareData.kext, BrcmPatchRAM3.kext, BT4LEContiunityFixup.kext).

You also have to disable the onboard Intel Bluetooth. 

In your USB-configuration this is the port HS14. Either add "uia_exclude=HS14" to your Boot-arguments or generate a USBPorts.kext with Hackintool and remove HS14. 

If it is still not working, download Bluetooth Explorer from Apple Developser (it is inside "Additional_Tools_for_Xcode_11.4.dmg"). 

Then start Bluetooth Explorer App, select Tools/HCI Controller Selector. Then you should be able to see your Bluetooth adapter e.g. Apple BRCM. Select it and press "Activate". If it is marked as "Active" it is working.

## Radeonboost.kext

The Radeonboost.kext improves the Graphics performance of AMD Radeon cards. I have a Radeon VII and it improved the OpenCL performance by 22% and in Metal by 38%. According to benchmarks with Geekbench 5.1.0.

# Installation notes
1. Create an MacOS Catalina 10.15.4 Installation Stick (just google it)
2. Delete Installinfo.plist:
  - Open the "Install macOS Catalina" Disk
  - Right Click on the package "Install macOS Catalina"
  - Click on "Package Contents"
  - Then navigate to Contents > SharedSupport
  - Delete the Installlnfo.plist
3. Mount the EFI partition of the Installation Disk (I use Hackintool to mount EFIs)
4. Copy my EFI folder to the root of the EFI-partition
5. Go to EFI/OC and open the config.plist with a plist Editor (I use "PLIST Editor" from the app store)
6. Within the config.plist navigate to PlatformInfo/Generic and paste your serials for MLB, SystemSerialNumber and SystemUUID. You can generate them with the tool CloverConfigurator.


Best,
Chris 
aka SchmockLord

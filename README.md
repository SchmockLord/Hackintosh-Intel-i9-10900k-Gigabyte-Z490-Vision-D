# Hackintosh-Intel-i9-10900k-Gigabyte-Z490-Vision-D

Hello folks,

I have successfully installed MacOS Catalina 10.15.4 on my i9-10900k running on a Gigabyte Z490 Vision D.

You can find my EFI folder in this repository.

I will update this Build in the next days. The Build is very fresh (3h after the first successfull installation).

SMBIOS=MacBookAir9,1

OpenCore 0.5.8

# Hardware:
- Intel i9 10900k
- Gigabyte Z490 Vision D
- Radeon VII
- 32GB 

# Working:
- [x] Wifi and Bluetooth (via BCM94360CD using a MQUPIN fenvi T919 Wireless Card)
- [x] Audio (AppleALC.kext, layout-id=7, device-id=0xA170, FakeID.kext, FakePCIID_Intel_HDMI_Audio.kext)
- [x] Sleep/Wake
- [x] Shutdown
- [x] Restart

## Bluetooth:
You need a natively supported Bluetooth card to use Airdrop, Unlock with Apple Watch etc.

I used the MQUPIN fenvi T919 Wireless Card. It has natively supported WiFi and Bluetooth. 

No further kexts needed (no AirportBrcmFixup.kext, BrcmBluetoothInjector.kext, BrcmFirmwareData.kext, BrcmPatchRAM3.kext, BT4LEContiunityFixup.kext).

You also have to disable the onboard Intel Bluetooth. 

In your USB-configuration this is the port HS14. Either add "uia_exclude=HS14" to your Boot-arguments or generate a USBPorts.kext with Hackintool and remove HS14. 

If it is still not working, download Bluetooth Explorer from Apple Developser (it is inside "Additional_Tools_for_Xcode_11.4.dmg"). 

Then start Bluetooth Explorer App, select Tools/HCI Controller Selector. Then you should be able to see your Bluetooth adapter e.g. Apple BRCM. Select it and press "Activate". If it is marked as "Active" it is working.

# Not working so far:
- [ ] Thunderbolt (update soon)
- [ ] Ethernet (update soon)


# Installation notes:
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

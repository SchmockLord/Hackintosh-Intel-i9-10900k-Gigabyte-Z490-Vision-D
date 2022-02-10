# Hackintosh-Intel-i9-10900k-Gigabyte-Z490-Vision-D

## USB Port Configuration

From Feb-2022 on, I don't use the Kext-based USB-configuration anymore. Instead, we use the USB-Port configuration via SSDT (SSDT-USB-Ports-Z490-VisionD.aml). 

The benefit of this is, that we don't need specific kexts for each SMBIOS (iMac20,2; iMacPro1,1 etc.) and it is the cleanest way of doing the USB-Port Mapping.

### My USB-port configuration ###

![USB-Port Configuration](Docs/USB-port-Configuration-Release-v5.3.png)

### HowTo change the USB-port configuration ###

In my SSDT you will see the comments for each port, some are enabled, some are disabled.

Per port you have two relevant methods: GUPC and GPLD (they are Gigabyte methods that call standard methods _UPC: USB port Capabilities and _PLD: Physical Location of Device)

e.g. GUPC (One, 0x03) means this port is enabled (one) and is a USB3-Type A (0x03) The first variable means enabled/disabled (one or 0xFF/zero or 0x00), the second variable describes the port itself.

zero is the same as 0x00
one is the same as 0xFF

Port types:
0x00 or zero: standard USB2 port (usually black)
0x03: USB3 Type A (usually blue, red or yellow)
0x09: Type-C with switch, where it doesn't matter which direction you plug the device in, it is always the same port.
0x0A: Type-C without switch, where there are used two ports, each for one direction.
0xFF: internal devices used for RGB, Audio, Bluetooth etc.

GPLD-method describes where the port sits. E.g. GPLD (One, 0x09) means this port is available on this board (one) and has the location HS09 (0x09). HS11 e.g. would be (0x0B). SS ports start with 1 e.g. SS01 is (0x11), SS10 (0x1A).

If you don't know the Hex-names of the ports, you can use Hackintool, e.g. Decimal 9 is also Hex 9 but 10 is A:
![Screen Shot 2022-02-10 at 12 01 54](https://user-images.githubusercontent.com/19785918/153393913-d64e66da-6dfc-4762-94e5-6418b84d95b6.png)


If you disable ports for macOS, you should wrap this like this, so Windows e.g. would use the Else-case where this port is enabled (0xFF) and has is a type-C with switch (0x09):

If (_OSI ("Darwin"))
{
Return (GUPC (Zero, Zero))
}
Else
{
Return (GUPC (0xFF, 0x09))
}

You also need to Delete the original ACPI-table for the USB-Port Mapping: SSDT-7-xh_cmsd4.aml 

![Screen Shot 2022-02-10 at 11 58 13](https://user-images.githubusercontent.com/19785918/153393316-97496e56-d6c0-44fc-a62b-c43a9f1656d0.png)




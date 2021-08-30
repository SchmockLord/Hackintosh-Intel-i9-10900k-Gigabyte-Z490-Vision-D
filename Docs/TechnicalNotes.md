# Technical Notes

#### Technical Note: Installation > GUID Format

You can see the format of a drive via the terminal using `diskutil list`. If your `/dev/disk<n>` is not listed as `GUID_partition_scheme` you can use the command line `diskutil eraseDisk /dev/disk<n> GPT JHFS+` to re-format and erase it as GUID partitioned. (See [GPT terminology in dortania](https://dortania.github.io/OpenCore-Install-Guide/terminology.html))

#### Technical Note: Installation > Serial Numbers

You can use CloverConfigurator to generate unique serial numbers for:

 - MLB
 - SystemSerialNumber
 - SystemUUID

The reason you want unique serial numbers is so that things like iMessage recognize your hackintosh as a valid Mac and the tool will function. For details see this guide: [an idiots guide to iMessage](https://www.tonymacx86.com/threads/an-idiots-guide-to-imessage.196827/)
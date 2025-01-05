> **This page is not considered to be complete yet and as such may be subject to changes.**

U-Boot is an open source bootloader commonly used for booting up applications in Embedded Systems. It is designed to initialised hardware and load various different operating systems.

---
# Where does U-Boot actually come into play?

So the [first](./First%20few%20stages%20of%20a%20Bootloader#Stage%201%20-%20Hardware%20Initialisation) and [second](./First%20few%20stages%20of%20a%20Bootloader#Stage%202%20-%20Bootloader%20mode%20or%20application%20mode) parts of the initial boot process are usually taken care of by the BIOS/UEFI or the system chip manufacturer.

Then the next few steps i.e. [setting up the execution environment](./First%20few%20stages%20of%20a%20Bootloader#Stage%203%20-%20Startup%20Code) and [loading the Operating System](./First%20few%20stages%20of%20a%20Bootloader#Stage%204%20-%20Loading%20the%20OS) are managed by U-Boot itself.

## Major role of Primary Bootloader (Embedded Systems)
After the setting up the very basic hardware such as clocks, interrupt and exception vectors and SDRAM (Synchronous Dynamic Random Access Memory), the primary bootloader:
+ Decomposes the U-Boot from flash (or other supported types of memory) to the RAM.
+ Passes the execution control over to U-Boot.

## Major role of U-Boot
+ Configures the Ethernet MAC address, flash, and serial console.
+ Loads the settings stored as environment variables into non-volatile memory.
+ After a few seconds (a length of time you can program), automatically boots the pre-installed kernel.
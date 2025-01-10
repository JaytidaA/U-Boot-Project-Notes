U-Boot has a set of built in commands for booting the system, managing memory, and updating an embedded system's firmware.

We have to make use of these commands at the monitor prompt during the startup process.

# Monitor
U-Boot has a command shell (like the Bourne shell `sh`), which is called the monitor, where we can make use of U-Boot commands to create a customised boot process.

---
Let us now discuss a few important commands and their uses. I wont be listing the uses of all the commands because it would be far too time consuming, you can refer to set of commands from the official U-Boot [docs](https://docs.u-boot.org/en/latest/usage/index.html#shell-commands) or the help manual credited at the end.
## help
This command displays the list of all available commands for the U-Boot monitor for your hardware.
```shell
$ help
```
```
?       - alias for help
autoscr - run script from memory
base    - print or set address offset
bdinfo  - print Board Info structure
boot    - boot default, i.e., run 'bootcmd'
...
```

For more information about a particular command, use the syntax `help <comname>`
```shell
help run
```
```
run var [...]
	- run the commands in the environment variable(s) 'var'
```

We will now discuss commands by common functionalities and group them together, most of the commands have simple straightforward names which define what they do.

## Information commands
To get information, use these commands:
+ `bdinfo`: Board information.
+ `coninfo`: Console devices and information.
+ `fatinfo`: Displays information about a FAT partition.

There are more useful commands in this section, you can read about them in the docs.

## MII commands
MII stands for Media Independent Interface, basically it is a method for communication over Ethernet. This is an older subsystem which was not used as much, so the functionality has been abstracted in different components.

These commands were mostly used to access the Ethernet PHY.

## Network commands
These include `bootp`, `tftpboot`, `dhcp`, `nfs`, `rarpboot` and `ping`.
+ Ping is self explanatory but the others are just commands to set up a connection to a predefined network specified in the environment using an IP address and booting the image from that file.

## USB commands
The USB submodule provides us with the USB commands, which contains a bunch of helpful commands for displaying the USB port's information, reading from and loading images from over the USB connection.

## Memory commands
These contain several utility commands for comparing, reading from and writing to (flash memory), and overall management of the RAM.

## Serial Port commands
We use these commands to configure the serial line and work with it. e.g. setting the baud rate.

## I2C commands
I2C is a communication protocol which can achieve half-duplex modes of communication. We can use this set of commands to communicate over the I2C connections.

## Environment commands
These commands are used to create, edit, print, delete and save the environment variables. Almost all of them have the form: `env <do-something>` 

# Credits
+ Das U-Boot [docs](https://docs.u-boot.org/en/latest/usage/index.html#shell-commands)
+ Digi's [U-Boot reference manual](https://hub.digi.com/dp/path=/support/asset/u-boot-reference-manual/)
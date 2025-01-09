Although written in C, U-Boot supports user configuration via environment variables which can be made persistent by saving to persistent storage, example flash memory.

We can save and modify the environment variables by making use of the `env` command and its various different parameters and aliases. A few of the common ones are:

+ `env set`/`setenv [-f] name [value]`: Used to set environment variables when value is specified, or delete variables when not.
+ `env print`/`printenv [-a | name ...]` Used to print the value of an environment variable with the name `name`, if no name is specified and the `-a` flag is passed, then all of the environment variables and their values are listed.
+ `env edit name`: Take a wild guess.
+ `env save`: Saves the environment variables in persistent storage.
---
# Why are environment variables useful?
The environment variables are a set of variables which are used for various different purposes.

Consider a basic example of why environment variables are useful:
* If you would like to make use of almost any shell command in a UNIX-like operating system, you can directly type the name of the command. For example to show the current date and time.
```shell
date
```

* `date` is a veery vague name for a command. One would be using the name "date" to track important events, how does the shell know to make use of the correct date binary present in the `bin` folder of the user?
* This is where environment variables come in. There is a special variable called `PATH` which defines the list of folders to search for executable binaries.
* Environment variables are used for multiple purposes but their most important use is for **system configuration**.

---
# Text-based Environment
The default environment for the board is created using a plain text file called `<CONFIG_ENV_SOURCE_FILE>.env` placed at the path: `board/<vendor>/<board>/<CONFIG_ENV_SOURCE_FILE>.env` 

It is a plain text file which can be used to set environment variables.

The elements of the file should be of the form `var=value` or `var+=value` where we must ensure that the string `var=` appears on the first column of the new line.

We can make use of blank lines, white spaces, and `/* C-style multi-line comments */`. Normal C pre-processor directives and CONFIG defines present in the board config can be used as well.

Example:
```shell
stdout=serial
#ifdef CONFIG_VIDEO
stdout+=,vidconsole
#endif
bootcmd=
    /* U-Boot script for booting */

    if [ -z ${tftpserverip} ]; then
        echo "Use 'setenv tftpserverip a.b.c.d' to set IP address."; exit 1;
    fi

    usb start; setenv autoload n; bootp;
    tftpboot ${tftpserverip}:
    bootm
failed=
    /* Print a message when boot fails */
    echo "${CONFIG_SYS_BOARD} boot failed - please check your image"
    echo "Load address is ${CONFIG_SYS_LOAD_ADDR}"
```

In this example, we are setting the standard output to the serial port and optionally to the video console if the config has been defined.

We also set the `bootcmd` variable, this variable contains the steps to be followed to actually boot the image from the flash memory.

We then set the `failed` variable which defines what to do when booting fails, in this example we just log the outputs to the standard output using `echo` and tell the user to check the image.

> Keep in mind that we have just defined this variable, we have not used it anywhere and it won't be used by default if boot fails.

## Environment variable: `bootcmd`
As seen before, this variable is used to store the set of instructions to follow to actually load the kernel image from the flash to the DRAM and then boot it.

It usually contains instructions for loading the operating system kernel, an initramfs, or a device tree blob (DTB), and then booting the system.

In the above example, we check if the `tftp` (a file transfer protocol) server has been set up, and if it is, we load the file from the tftp server and start the tftp boot; if not then we exit with return code 1.

## Environment Variable: `bootargs`
`bootargs` contain the command line arguments to be passed to the kernel during boot.

These arguments define how the kernel should behave and interact with the hardware, root file-system, and other components.

```shell
bootargs=<arguments>
```
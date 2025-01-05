Before we start, we need to understand what a boot-loader is and why do we use it.

The boot-loader is the part of **machine code or instructions (usually written in assembly) which runs from the point the power button is turned on to the time the `main` function of our written code** is called.

On many motherboards or in integrated systems, the microprocessor or the micro-controller does not remember the neighbours (peripherals). So to remind it of these neighbours and bring the entire system into a fully usable state, we make use of a boot-loader.

---
We will consider examples of a regular PC booting and a SoC micro-controller being turned on for use.

After turning on a micro-controller, most of the time, the only "memory" it retains is a *singular instruction* it should execute after it is turned on, which is called the RESET code.

The RESET code is only useful for transferring execution over to the Hardware initialisation code which can be considered to be the first stage of the booting process.

# Stage 1 - Hardware Initialisation
The code which runs on your computer for the short period of time after pushing the power button and before the computer monitor lights up with the manufacturer's logo is known as the hardware initialisation code.

## What this piece of code does?
+ It wakes the microprocessor up.
+ It "introduces" the microprocessor to the critical peripherals.
+ Microprocessor in turn wakes up the critical peripherals. (monitor, graphics card, keyboard, mouse)

The introduction of microprocessors to peripherals is necessary because once it has been powered off, it loses all of its volatile memory and only remembers the RESET code.

# Stage 2 - Bootloader mode or application mode
Once the microprocessor has been woken up along with the peripherals, the second stage of the boot-loader starts.

Now, a decision needs to be made by the user, to go into either of the two modes:
1. "default" or "application" mode
2. "special" or "boot-loader" mode

On a PC, the default mode takes you to the login screen or login manager whereas the boot-loader mode takes you to the BIOS/UEFI settings.

## How to make this decision?
1. <u>Personal Computers</u>
   The User of the system can decide to enter the "special" mode by *pressing* a specific *set of computer keys* (usually decided by the Motherboard manufacturer).
   
   e.g. on HP systems, to go into the BIOS setting, one presses the "ESC" key repeatedly to get a bunch of menu options, one of which is to enter the BIOS/UEFI settings.
   
   This decision is left to the user for a short amount of time, after which the system decides to enter the "default" or "application" mode on its own.

2. <u>Embedded Systems</u>
   In embedded systems, the simplest method to get input is *via the GPIO pins*, depending on the value of a specific GPIO pin, the system goes into "application" or "boot-loader" mode.
   
   Since the GPIO pins are usually suspect to noise, another method to make this decision is to read the data present in a non-volatile part of memory (location 0) and make the decision based on the value at this memory location.

## Use of bootloader mode
On typical PCs, you can use the boot-loader to set up the things such as Fan Speed, RAM speed, the CPU speed and the disk partition to boot of off. For embedded systems, the user can perform tasks such as selecting the default options for application software to use, reflash the code or update the application software.

# Stage 3 - Startup Code
On microprocessor systems, the microprocessor executes the **startup code** to make the system ready. The main purpose of this code is to **prepare the execution environment for programs written in high level languages.** 
The startup code performs the following tasks:
+ Allocates space for and copies the local variables into the RAM
+ Stack and stack pointer is initialised.
+ Heap is initialised.
+ `main` is called in the program.

# Stage 4 - Loading the OS
Once the environment is ready, the next step is to start the operating system. This is optional in embedded systems as most of them are designed to work without one.

The brief time in between the boot screen and login screen (login manager, tty, sddm, gdm, lightdm, etc) is the time where the system executes the code for starting the Operating System.

In this time, all the required drivers are loaded and the daemons are set up and control is passed over to the Operating System.

# Credits
* Balaji Gunasekaran. "Bootloader And Stages of Booting Process Explained!" July 3rd, 2019. [URL](https://embeddedinventor.com/embedded-bootloader-and-booting-process-explained/ "Bootloader And Stages of Booting Process Explained!")
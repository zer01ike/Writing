#The Linux boot process
## Boot sequence
 * system startup
 * bootloader
 * bootloader 2
 * kernel
 * init

## overview
BIOS->to find the boot devices

Boot devices-> to seed a single sector less than 512 bytes to RAM and Executed.

Boot Loader2 -> pass control to the kernel image, check the system hardware, enumerates the attached hardware devices, mounts the root device. 

kernel -> 

init -> user-space program starts, high-level system initialization.


## system startup
a bootstrap environment like U-Boot, RedBoot, MicroMonitor started to reside in speical region of flash memory on the target hardware and provide the means to download a Linux kernel image into falsh memory and susequently execute it.

### Steps:
0xFFFF0 BIOS started

next step : POST(power on self test) to check the perform of the hardware.

next step : local device enumeration and initialization.

### Attention:
After POST, BIOS will be flushed from memory, but the BIOS runtime services remain and are available to the target operating system.

BIOS runtime searchs the bootable devices in the order of perfernce defined by the complementary metal oxide semiconductor(CMOS) setting. 

Linux will boot from the sequence that are bootable device where the Master Boot Record(MBR) . MBR:512 bytes, located in the first sector on the disk.

After MBR is loaded into RAM, the BIOS yields control to it.

## Boot loader 1
### structure of the MBR
512 bytes 
1~446 bytes : primary boot loader contain both executable code and error message text.

Next 64 bytes : partition table contain four partitions (sixtenn bytes each)

End 2 bytes : Magic number which is a validation check of the MBR

### task
find and load the secondary boot loader.

how to do ? 
look through the partition table for an activce partition.
when find it, scan remaining partitions to ensure they're all inactive. When this is verified, the partition's boot record is read from the device into RAM and excuted.

## Boot loader 2
### task
load the Linux kernel and optional inital RAM disk

LILO(Linux Loader) it has some disadvantages 

GRand Unified Bootloader(GRUB)

GRUB can load a linux kernel from an ext2 or ext3 file system throughing stage 1.5 which will understand the particular file system containing the Linux kernel image.

After Boot loader 2 load in to the memory, the file system is consulted, and the default kernel image and initrd image are loaded into memory.

## Kernel
begin with ./arch/i386/boot/head.S : do some basic hardware setup.

then ./arch/i386/boot/compressed/head.S startup_32 :
set up a basic environment and clears the Bolock Started by Symbols(BSS)

then ./arch/i386/boot/compressed/misc.c decompress_kernel : 
decompress the kernel into the memory

then ./arch/i386/kernel/head.S setartup_32:
initialize the page tables and enable the memory paging.

then init/main.c start_kernel :
take you to the non-architecture specific Linux kernel.
 
End ./arch/i386/kernel/process.c kernel_thread :
a long list of initialization functions are called to set up interrupts, perform further memory configuration, and load the initial RAM disk.

Finally ./init/main.c cup_idle :
start idle task and scheduler can take control.

## init 
After the kernel is booted and initialized, the kernel starts the first user-space application. 

In a desktop Linux system, the first application started is commonly /sbin/init.

Rarely do embedded systems require the extensive initialization provided by init(/etc/inittab).you can invoke a simple shell scrpit that start the necessary embedded applications.



###Installation Notes

[Manually reformat an SD card and install Linux (Linux)](https://github.com/rixwoodling/raspberry-pi/blob/master/test.md#head)  
[Manually reformat an SD card and install Linux (Mac)](https://github.com/rixwoodling/raspberry-pi/blob/master/test.md#head)  

===
####Step 1 - Reformatting an SD card for the Raspberry Pi

Start with an empty SD card. (If not, check out part X for steps to remove all data.)
Setting up a partition with terminal is a two-part process.
In part A, a new partition is created on the SD card. 
In part B, the partition is formatted with FAT32 (or FAT16).
In part C, an ext4 type partition is created and formatted.
In part X, the SD partitions are removed and the SD is erased merely for the sake of knowhow.

===
#####A. Pre-Partition/Formatting Steps

1. Insert SD card. With Terminal open, type ```sudo fdisk -l``` or ```sudo parted```.

```sudo fdisk -l```
```bash
Disk /dev/sda: 80.0 GB, 80026361856 bytes
255 heads, 63 sectors/track, 9729 cylinders, total 156301488 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x0000acbc

   Device Boot      Start         End      Blocks   Id  System
/dev/sda1   *        2048   152147967    76072960   83  Linux
/dev/sda2       152150014   156301311     2075649    5  Extended
/dev/sda5       152150016   156301311     2075648   82  Linux swap / Solaris

Disk /dev/mmcblk0: 15.9 GB, 15931539456 bytes
4 heads, 16 sectors/track, 486192 cylinders, total 31116288 sectors
Units = sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x0005593a

        Device Boot      Start         End      Blocks   Id  System
        
```
Make note of the SD location: /dev/mmcblk0

2. Create a new partition. Type ```sudo fdisk /dev/mmcblk0``` 
3. When prompted with "Command (m for help): " type ```m```
4. Double check there is no current partition. Type ```p```
5. Create a new partition. Type ```n```
6. When prompted with... Type ```p``` to create a Primary partition type.
	Partition type:
   	   p   primary (0 primary, 0 extended, 4 free)
           e   extended
	Select (default p): 
7. Partition: ```1```
8. First sector: ```2048```
9. Last sector: ```+65536K``` (for some reason +100M doesn't work)
   # For the root system, keep this number between +30M to +100M)

9.5 There's an inbetween step that appears unneccessary due the partition being formatted later on, but interesting nontheless. Also not sure if LBA flags have any effect with Linux.
	- Type ```t``` and then ```l```.
 	- Select ```c``` for W95 FAT32 (LBA)

10. If desired, type ```p``` to see the partition ready to be written.
11. Finally, and most importantly, type ```w``` to "write table to disk and exit"

========================
#####B. Formatting the Partition for FAT32

1. Make note of the new partition that has been created. /dev/mmcblk0p1
2. Unmount mmcblk0p1 with ```umount /dev/mmcblk0p1```
3. Verify dosfstools is installed. ```sudo apt-get install dosfstools``` if not.
4. Type ```sudo mkdosfs -F 32 -I /dev/mmcblk0p1```

When finished, type ```sudo parted /dev/mmcblk0``` then ```print all free``` or ```print free``` when prompted to see the new partition as well as the unallocated space left on the SD card. 

```bash
Model: SD SU16G (sd/mmc)
Disk /dev/mmcblk0: 15.9GB
Sector size (logical/physical): 512B/512B
Partition Table: msdos

Number  Start   End     Size    Type     File system  Flags
        8192B   1049kB  1040kB           Free Space
 1      1049kB  68.2MB  67.1MB  primary  fat32        lba
        68.2MB  15.9GB  15.9GB           Free Space
```
===
#####C. Creating the future /home Directory Partition
1. Type ```sudo fdisk /dev/mmcblk0```
2. Type ```n``` for a new partition.
3. Type ```p``` for a new Primary partition type.
4. First sector: Hit 'enter' to accept the default value. It should automatically queue to the next available sector after the first partition that was made.
5. Last sector: This time, type ```+3G``` to make a 3 gigabyte partition.
6. Type ```w``` to finish the partition and exit.
7. Format the partition with ```sudo mkfs.ext4 /dev/mmcblk0p2```
8. Lastly, double-check with ```sudo parted /dev/mmcblk0``` and then ```print free```.

===
#####X. Erasing Partitions and Starting Again

Once a partition has been formatted they can be erased with fdisk.
1. In Terminal, type ```sudo fdisk /dev/mmcblk0```
2. When prompted for a command, type ```d``` for "delete partition".
3. When prompted for partition number, type any partition number.
4. Finally, type ```w``` to commit changes.


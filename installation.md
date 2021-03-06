###Installation Notes

[Manually reformat an SD card and install Ghostbang Linux (Linux)](https://github.com/rixwoodling/raspberry-pi/blob/master/test.md#head)  
[Manually reformat an SD card and install Ghostbang Linux (Mac)](https://github.com/rixwoodling/raspberry-pi/blob/master/test.md#head)  

---
<sup>Latest Downloads</sup>  
[![downloads](https://camo.githubusercontent.com/82b1476790cd388cf2d4a89ced92e9a73e0c19a4/68747470733a2f2f696d672e736869656c64732e696f2f62616467652f76616e696c6c612d323031352e30382e30362d3045424645392e737667)](http://creativecommons.org/
    licenses/by-nc-nd/3.0/) <sup>```download this one if you want the minimum```</sup>  
[![downloads](https://img.shields.io/badge/dragon%20fruit-in%20development-ff69b4.svg)](http://creativecommons.org/
    licenses/by-nc-nd/3.0/) <sup>```experimental; unavailable at the moment```</sup>    

<sub><i>Installation instructions are found [here](http://www.sudo.ws/). </i></sub>

---

####Step 1 - Reformatting an SD card for the Raspberry Pi

Start with an empty SD card. (If not, check out part X for steps to remove all data.)
Setting up a partition with terminal is a two-part process.
In part A, a new partition is created on the SD card. 
In part B, the partition is formatted with FAT32 (or FAT16).
In part C, an ext4 type partition is created and formatted.
In part X, the SD partitions are removed and the SD is erased merely for the sake of knowhow.

===
#####A. Pre-Partition/Formatting Steps

1 - Insert SD card. With Terminal open, type ```sudo fdisk -l``` or ```sudo parted```.  

```sudo fdisk -l```  
> <sub>You'll probably see something more complicated than the abridged output below.</sub>
```
Disk /dev/sda: 80.0 GB, 80026361856 bytes
Disk /dev/mmcblk0: 15.9 GB, 15931539456 bytes
```  
> <sup>Make note of the SD location, which, for me is:</i> ```/dev/mmcblk0```.</sup>  
  
2 - Create a new partition. Type ```sudo fdisk /dev/mmcblk0```  
3 - When prompted with "Command (m for help): " type ```m```  
4 - Double check there is no current partition. Type ```p```  
5 - Create a new partition. Type ```n```  
6 - Create a partition type. Type ```p```  
> <sub>Make sure there are 4 primary partitions free.</sub>
```
Partition type:
   p   primary (0 primary, 0 extended, 4 free)  
   e   extended  
Select (default p):   
```
>

7 - Partition: ```1```  
8 - First sector: ```2048```  
9 - Last sector: ```+65536K``` (for some reason +100M doesn't work)  
> For the root system, keep this number between +30M to +100M)

9.5 - There's an inbetween step that appears unneccessary due the partition being formatted later on, but interesting nontheless. Also not sure if LBA flags have any effect with Linux.
	- Type ```t``` and then ```l```.
 	- Select ```c``` for W95 FAT32 (LBA)

10 - If desired, type ```p``` to see the partition ready to be written.  
11 - Finally, and most importantly, type ```w``` to "write table to disk and exit"

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


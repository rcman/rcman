# All things Linux and RISC-V - Banana PI-F3  - Lechee PI 4A  - Star Five Vision 2
# Ubuntu 24.04 on BPI-F3 from SD-Card and running from NVME
# Updated Aug 21st 2024
<br>

A little about me....I'm an old school guy who likes things simple.  I've got a lot of systems, ranging from my 1950X threadripper, Mac Pro, iMac and all are running Linux usually Ubuntu. <br>
<br>
Three RISC-V boards, a Banana PI-F3, Lechee PI 4A Laptop and Star five vision 2. I'll be honest it's been a struggle using these RISC-V boards. They're not well supported getting them installed/upgraded to Ubuntu has been difficult.<br>
<br>
The only one that's running Ubuntu (24.10) right from the NVME is the Star Five Vision 2 but the HDMI still doesn't work. I've ordered some HDMI 2.1 cables to see if that makes a difference so we'll see.<br>
<br>
Looking to start my Youtube channel soon. 
<br>
<br>

**Here's a description how I have my Banana PI-F3 Running Ubuntu 24.04.  This should also work with 24.10.  I release it would be easier to upload my SD Card image so I'll do that shortly.** <br>


**The Short Version**

Download the initrd.gz from the files [Image](https://github.com/rcman/BPI-F3/blob/main/files/initrd.gz) directory. Rename it to the same name of the initrd in the boot directory, I would backup the original first. Make sure you run sync from the command line to make sure everthing is written to the SD Card.  Burn the Ubuntu image (link below) to m.2. Your system will boot from Micro SD Card and then run from m.2
<br>

**Long Version**
<br>
Ubuntu 24.04 is now running on my BPI-F3. Will be working on a video for YouTube soon.

This should work for any version of Linux, this has only been tested with Ubuntu 24.04

**Getting Started**

Download the Bianbu [Image](https://drive.google.com/file/d/1WsmhTV6EIBS-wwhl4kwgR_v_N9DgiJ-C/view?usp=drive_link) and use your favorite tool to image it to micro SD card. 

Download the Ubuntu [Image](https://cdimage.ubuntu.com/releases/noble/release/ubuntu-24.04.1-preinstalled-server-riscv64.img.xz) Ubuntu 24.04 to the NVME  (NOTE: you will lose all your data) <br> 

Imaging to the NVME can be performed a couple differnet ways. You copy copy the image from another system to your risc machine's SD Card, or use an image program like raspberry pi Imager or Balena Etcher. You can buy a USB to m.2 adapter which you can purchase on Amazon for about $20 dollars. 
<br>

This boot has only been verified on this version of Ubuntu. It should work for all versions of Linux you just need to know which partition is root(/).
After you've imaged Bianbu to the SD card. Re-insert it to your PC and mount partition. Run this command next.

**sudo mkdir /mnt/sd**

**sudo mount /dev/sdd5 /mnt/sd** <br> (or which ever drive letter yours shows up as. Mine shows up as sdd. if yours
shows up as SDA then mount /dev/sda5). You can determine which drive it is by running the command (**lsblk**)
Once mounted run the command to change directory.

**cd /mnt/sd**

Make a working directory in your home directory.

**mkdir ~/work**

Now copy the initrd-6.1.15 with the command below.<br>
**cp initrd.img-6-1-15 ~/work/**

Download
Copy the cpionew.sh Link below.
Download the [File](https://github.com/rcman/BPI-F3/blob/main/cpio/cpionew.sh) here and copy it to your work directory.
type this command to go there<br>

**cd ~/work**

you should already have the initrd.img-6.1.15 in this directory along with the cpionew.sh
type this command: 

**mkdir initrd-tree**

type this command

**cp initrd.img-6.1.15 initrd.gz**

now uncompress the initrd with this command: 

**./cpionew.sh -u**

this should extract the initrd to the initrd-tree directory
Change to that directory with this command

**cd initrd-tree**

Download the [init](https://github.com/rcman/BPI-F3/blob/main/files/init) file located in the files directory. Replace the init in initrd-tree with the one you Downloaded. Go back one directory by typing:

**cd ..**

Now re-compress the initrd with this command

**./cpionew.sh -r**

Now run this command

**cp initrd.gz initrd.img-6.1.15**

with the SD card still mounted as above run this command

**sudo cp initrd.img-6.1.15 /mnt/sd/**

type this command

**sync**

and then type cd to change back to your home directory
now unmount the sd card with this command

**sudo umount /mnt/sd** 

remove the sd card and put it in the BPI-F3 machine and turn it on. It should boot to Ubuntu located on the NVME
 
If you need help let me know.
Thanks
Franco
![BPI-F3 Running Ubuntu 24.04](https://i.imgur.com/s9crx20.png)
<br><br>
# Project 2 Fixing the kernel
<br>
https://github.com/TroyMitchell911/bpi-f3-linux-6.6
<br>
The link below is to show the modules and network drivers needed to boot.<br>
https://github.com/jellyterra/bpi-f3-archlinux
<br>

**Fixing the boot so it will always boot**
<br>
https://gitlab.com/rkraevskiy/ubootpubkey/-/blob/master/README?ref_type=heads


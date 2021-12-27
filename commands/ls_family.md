*ls family commands are usually inside /usr/bin, you can list them using: ls -l /usr/bin/ls\**

### ls 

list out files & folders under a certain folder, if no folder is specified, it default to current folder

```sh
# simple usage
ls
# colored output (this usually seperates folder from regular file)
ls --color=auto
# by default, ls won't list out hidden files(file starts with a dot), to list them, using -a options
ls -a
# "ls -a" will also list out current folder as "." & its parent folder as "..", which is often unnecessary, to elliminate them, use -A
ls -A
# list items in their long form
ls -l
# list items in their long form, with human-readable file size
ls -lh
```

```sh
# sort items 
ls --sort=size # sort by file size
ls -S # short form

ls --sort=time # sort by last modified time
ls -t # short form

ls --sort=extension # sort by extension
ls -X # short form
```

```sh
# you probably want to use this by default
ls -AXlh --color=auto
```

### lscpu

lscpu list out information about your cpu, it's based on file /proc/cpuinfo, but much concise.

the following is an example of `lscpu` output

```
Architecture:                    x86_64
CPU op-mode(s):                  32-bit, 64-bit
Byte Order:                      Little Endian
Address sizes:                   48 bits physical, 48 bits virtual
CPU(s):                          16
On-line CPU(s) list:             0-15
Thread(s) per core:              2
Core(s) per socket:              8
Socket(s):                       1
NUMA node(s):                    1
Vendor ID:                       AuthenticAMD
CPU family:                      25
Model:                           80
Model name:                      AMD Ryzen 7 5800H with Radeon Graphics
Stepping:                        0
Frequency boost:                 enabled
CPU MHz:                         1200.000
CPU max MHz:                     4462.5000
CPU min MHz:                     1200.0000
BogoMIPS:                        6387.36
Virtualization:                  AMD-V
L1d cache:                       256 KiB
L1i cache:                       256 KiB
L2 cache:                        4 MiB
L3 cache:                        16 MiB
NUMA node0 CPU(s):               0-15
```

note that the CPU count is 16, it doesn't mean I have 16 physical CPU on my motherboard, here the CPU refers to logical CPU, the ones that can be recognized & used by the operating system

### lsblk

lsblk stands for "list block devices", it's useful if you want to list out storage devices (such as disks , usb flash drive, sd card, etc)

lsblk list out devices & their partitions in a tree like format & shows the mountpoint of mounted partitions

the following is an example of `lsblk` output

``` 
NAME        MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
sda           8:0    0   477G  0 disk /media/rz/Infinity
sdb           8:16   1   7.2G  0 disk 
└─sdb1        8:17   1   7.2G  0 part /media/rz/Photography
mmcblk0     179:0    0  59.5G  0 disk 
└─mmcblk0p1 179:1    0  59.5G  0 part /media/rz/3635-3539
nvme0n1     259:0    0   477G  0 disk 
├─nvme0n1p1 259:1    0   260M  0 part /boot/efi
├─nvme0n1p2 259:2    0    16M  0 part 
├─nvme0n1p3 259:3    0   200G  0 part 
├─nvme0n1p4 259:4    0 140.2G  0 part 
├─nvme0n1p5 259:5    0  1000M  0 part 
└─nvme0n1p6 259:6    0 135.5G  0 part /
```

from the output, we know that out linux system (mountpoint /) is a parition called "nvme0n1p6" on disk "nvme0n1"

we also know we have 3 external storage devices & can access file in them through their mountpoint

you can use "-f" option to get info about filesystem of each partition & their usage

the following is an example of `lsblk -f` output

```
NAME        FSTYPE   LABEL       UUID                                 FSAVAIL FSUSE% MOUNTPOINT
sda         ext4     Infinity    5cd96636-4c7d-4719-955f-c40c4023e1fa    444G     0% /media/rz/Infinity
sdb                                                                                  
└─sdb1      vfat     Photography 04F2-2AC7                               7.2G     0% /media/rz/Photography
mmcblk0                                                                              
└─mmcblk0p1 exfat                3635-3539                              59.5G     0% /media/rz/3635-3539
nvme0n1                                                                              
├─nvme0n1p1 vfat     SYSTEM_DRV  8827-B4A3                             222.1M    13% /boot/efi
├─nvme0n1p2                                                                          
├─nvme0n1p3 ntfs     Windows-SSD FE9028FF9028BFCF                                    
├─nvme0n1p4 ntfs     Data        6E049D25049CF0F7                                    
├─nvme0n1p5 ntfs     WINRE_DRV   DA56299656297503                                    
└─nvme0n1p6 ext4                 4fdc6bb3-7ae9-4f19-8ffd-6ebe4ce6bf63  106.8G    14% /
```

### lsmem 

a simple command to print out how much physcial memory you have on your system

here's an example output

```
RANGE                                  SIZE  STATE REMOVABLE  BLOCK
0x0000000000000000-0x00000000cfffffff  3.3G online       yes   0-25
0x0000000100000000-0x000000072fffffff 24.8G online       yes 32-229

Memory block size:       128M
Total online memory:      28G
Total offline memory:      0B
```

### lsusb

lsusb prints all usb devices connected to your system

example output:

```
Bus 004 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 003 Device 003: ID 04f2:b71f Chicony Electronics Co., Ltd Integrated Camera
Bus 003 Device 002: ID 046d:c545 Logitech, Inc. USB Receiver
Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 002 Device 007: ID 0bda:8153 Realtek Semiconductor Corp. RTL8153 Gigabit Ethernet Adapter
Bus 002 Device 006: ID 05e3:0749 Genesys Logic, Inc. USB3.0 Hub             
Bus 002 Device 005: ID 0bda:0411 Realtek Semiconductor Corp. 
Bus 002 Device 004: ID 152d:0578 JMicron Technology Corp. / JMicron USA Technology Corp. JMS567 SATA 6Gb/s bridge
Bus 002 Device 003: ID 2109:0817 VIA Labs, Inc. USB3.0 Hub             
Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
Bus 001 Device 004: ID 04f3:0c4b Elan Microelectronics Corp. ELAN:Fingerprint
Bus 001 Device 003: ID 8087:0029 Intel Corp. 
Bus 001 Device 002: ID 046d:c08b Logitech, Inc. G502 HERO Gaming Mouse
Bus 001 Device 008: ID 2109:8817 VIA Labs, Inc. 
Bus 001 Device 007: ID 0bda:5411 Realtek Semiconductor Corp. ELAN:Fingerprint
Bus 001 Device 006: ID 1a40:0801 Terminus Technology Inc. 
Bus 001 Device 005: ID 2109:2817 VIA Labs, Inc. USB2.0 Hub             
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```

in this example, if you `grep -i 'logitech'` you get

```
Bus 003 Device 002: ID 046d:c545 Logitech, Inc. USB Receiver
Bus 001 Device 002: ID 046d:c08b Logitech, Inc. G502 HERO Gaming Mouse
``

then we know, we have 2 logotech devices connected via usb, one is a mouse, another one is a receiver, in my case, this receiver connectes to my keyboard wirelessly.



TODO: add `lspci` & `lsof`, I'm still learning about them :(

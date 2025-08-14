- A file system is an organized structure of data-holding files and directories residing on storage device. The process of adding new file system into existing directories is called mounting and the
directory is called mount point. Hard disks and other storage device are normally divided into partitions. In Linux, Different types of hard disks has different representations for their partitions.

- **== Types of Hard disks and there partition representation:**

<img width="792" height="146" alt="image" src="https://github.com/user-attachments/assets/0c64b421-4aa2-444b-b18b-bbec48d93ac0" />

---
### HardDisk Representation

- These representation are the special files called as block device. The block devices are stored in the `/dev` directory. Disk Partitioning is the method of dividing hard drives into multiple logical
storage units referred to as partitions. There are two schemes of disk partitioning: 1. MBR partitioning scheme 2. GPT partitioning scheme.

- `MBR Partitioning Scheme`: Master Boot Record partitioning scheme (MBR) dictates how disks should be partitioned on system. MBR uses the standard BIOS partition table thus it has size limit of 2TB. MBR
has size 512 bytes among which 64 bytes are used for partition table info. Each partition creation requires 16bytes thus MBR scheme supports a maximum of four primary partitions (or 3 primary and 1 extended).

- `GPT Partitioning Scheme`: GUID Partition Table (GPT) overcomes from limitations of the MBR partition. It has size limit of 8 ZB and making more than four primary partition is also possible.

- **== Types of Partitions:**

- `Primary`: A primary partition is in which operating system can be installed. In MBR, maximum four primary partition can be create. The primary partition which is use to boot the system is called an
active partition. (Active partition is the partition from which operating system is loaded.

- `Extended`: Extended partition breaks the limit of four partition. Using extended partition we can create no. of logical partitions. Extended partition holds logical partition. Only one extended partition is
allowed.

- `Logical`: Logical Partitions are created inside the extended partition. RHEL 6 supports maximum of 12 logical partitions whereas RHEL 7 supports maximum of 60 logical partitions. To create logical
partition, first you must create extended partition.

---
## MANAGING MBR PARTITION:

- For MBR partitioning scheme, fdisk partition editor is used.

- Creating Partition

```
[root@localhost Desktop]# fdisk /dev/sdb
Welcome to fdisk (util-linux 2.23.2).

Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Device does not contain a recognized partition table
Building a new DOS disklabel with disk identifier 0x56d50362.

Command (m for help):
```
---
2. Above step opens MBR partition editor, enter m to get help about commands.

```
Command (m for help): m
Command action
a toggle a bootable flag
b edit bsd disklabel
c toggle the dos compatibility flag
d delete a partition
g create a new empty GPT partition table
G create an IRIX (SGI) partition table
l list known partition types
m print this menu
n add a new partition
o create a new empty DOS partition table
p print the partition table
q quit without saving changes
s create a new empty Sun disklabel
t change a partition's system id
u change display/entry units
v verify the partition table
w write table to disk and exit
x extra functionality (experts only)

Command (m for help):
```
---
3. Enter n to request new partition and give values of requesting fields.

```
Command (m for help): n
Partition type:
  p primary (0 primary, 0 extended, 4 free)
  e extended
Select (default p): p                                                              ---> select partition type as per above choice
Partition number (1-4, default 1): 1                                               ---> give partition number
First sector (2048-62914559, default 2048): 2048                                   ---> starting sector of partition
Last sector, +sectors or +size{K,M,G} (2048-62914559, default 62914559): +2G       ---> size of disk
Partition 1 of type Linux and of size 2 GiB is set
```
---
4. Toggle the partition if partition should have type other than Linux. ‘L’ will show list of partition type
```
Command (m for help): t
Selected partition 1
Hex code (type L to list all codes): L
```
---

5. Partition will not be created until the changes has been saved. Give ‘w’ command to save the changes.
```
Command (m for help): w
```
---

To view partitioned blocks

```
[root@localhost Desktop]# lsblk
```
---

To update partition table

```
[root@localhost Desktop]# partprobe
```
---

### File Systems

- A file system is the way in which files are named, stored, retrieved and organized on the storage device or partition. Following are some commonly used file systems in now a days

  - xfs – A high performance filesystem originally developed by Silicon Graphics that works extremely well with large files. This filesystem is default for RHEL 7. NASA still uses this file
system on their 300 TB server.

  - ext2 – ext2 filesystem was introduced in 1993 and it was the first default file system in several Linux file system. It overcomes the limitation of legacy ext file system. The maximum
supported size is 16GB to 2TB. Journaling feature is not available. ext2 normally is used in flash based storage like pendrives, sd cards, etc.

  - ext3 – It was introduced in 2001 with all the features of ext2 and additional journaling feature.
    It also provides facility to upgrade from ext2 to ext3 without having to backup and restore
    data. 

  - ext4 – It is the high anticipated ext3 successor. ext4 was introduced in 2008 with backward capabilities. It supports maximum file size of 16TB. It has option to turn off journaling feature.
  - vfat – Microsoft extended FAT filesystem.

---
- Assign file system to partition

```
[root@localhost Desktop]# mkfs.xfs /dev/sdb1
```
---
- OR

```
[root@localhost Desktop]# mkfs -t ext4 /dev/sdb1
```
---

- List assigned file system disks, (it shows filesystem as well as partition block id)
```
[root@localhost Desktop]# blkid
```
---

## Mounting Partition
- Mounting is process of adding partition in to the system am specific directory. The directory is called as mounting point. There are two methods of mounting, temporary mounting mount the
partition temporary which get unmounts automatically after the reboot where as permanent mounting allows to mount permanent.

- Temporary mount

```

```
<img width="856" height="541" alt="image" src="https://github.com/user-attachments/assets/fcb5b832-b3e6-4f2f-98d7-37f236e31096" />

---
### Unmounts Partition

- Temporary unmounting
```
[root@localhost Desktop]# umount /dev/sdb1
```
---
- Permanent Unmounting can be done by removing the entry from fstab file and perform #mount –a.

### Removing Partition

- Before removing partition, first unmounts all the partitions that you wants to remove. Then remove partition using fdisk partition editor.

```
[root@localhost Desktop]# fdisk /dev/sdb
Welcome to fdisk (util-linux 2.23.2).

Changes will remain in memory only, until you decide to write them.
Be careful before using the write command.

Command (m for help): d                               ---> d command is used to delete
partition
Partition number (1,2, default 2): 1                  ---> select partition no.(takes last
partition as default)
Partition 1 is deleted
```
---
### Swap partition

 - swap space in Linux is used when the amount of physical memory is getting full. If the system needs more memory resource and the RAM is full, all inactive pages in memory moved to swap space.
(swap should not be consider a replacement of RAM).

- How to create swap space?

1. Step1: Create primary or logical partition

```
[root@localhost Desktop]# fdisk /dev/sdb -- create new partition
```
---

2. Step2: Assign swap file system

```
[root@localhost Desktop]# mkswap /dev/sdb1
```
---

3. Step3: Mount as swap partition

```
[root@localhost Desktop]# swapon /dev/sdb1                             --> mount swap partition temporary
[root@localhost Desktop]# vim /etc/fstab                               --> for permanent mount
/dev/sdb2 swap swap defaults 0 0                                       --> Entry for swap partition. Mount
point should be swap
```
---

- See swap partitions

```
[root@localhost Desktop]# swapon
```
---

- unmounts swap partition

```
[root@localhost Desktop]# swapoff /dev/sdb1
```
---






























































































































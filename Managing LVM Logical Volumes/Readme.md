# Logical Volume Management (LVM):

- Logical Volume Management or LVM is another disk partition management tool for the Linux. With LVM, physical disk partitions can be added to pools of space called volume groups. Logical
volumes are assigned space from volume groups as needed. Features of LVM.

  - More space can be to logical volume from the volume group while the volume is still in use.
  - More physical can be added to a volume group if the volume group begins to run out of space. The physical volumes can be from same or different disks.
  - Move data from one physical volume to another, so you can remove smaller disks and replace them with larger ones while the filesystem are still in use.
---
### Create Physical Volume

- Physical volumes are created from the existing partition,
```
[root@localhost Desktop]# pvcreate /dev/sdb1                         --> sdb1 is the existing
fdisk partition
```
---
- List Physical volumes
```
[root@localhost Desktop]# pvs                                          --> list of physical volumes
[root@localhost Desktop]# pvdisplay                                    --> show details of physical
```
---
### Create Volume Group

- Volume Group is the pool of space using virtual partitions
```
[root@localhost Desktop]# vgcreate vg_demo /dev/sdb1 /dev/sdb2                            --> create volume group using physical volumes
[root@localhost Desktop]# vgs                                                             --> list of volume groups
[root@localhost Desktop]# vgdisplay                                                       --> details of volume group
```





































































































































































































































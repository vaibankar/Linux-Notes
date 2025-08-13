# Linux File System Security:
  - Linux File System Security restricts user to access the files and directories. User require permissions to access files or directories. “ls -l” or “ll” command can be used to check security of any file or directory. Above command will display contents from directory along with its security details. Some of security attributes are shown below,
- Example
```
[root@ip-172-31-19-5 ~]# ll /root
total 8
-rw-------. 1 root root 6577 Jan 28 2019 original-ks.cfg
```
- To check security of any particular directory
```
[root@ip-172-31-19-5 ~]# ll -d /root
dr-xr-x---. 3 root root 181 Nov 5 10:46 /root
```
- Above example display contents from directory along with its security details. It contains ten fields as mentioned below

<img width="631" height="71" alt="image" src="https://github.com/user-attachments/assets/57bb1180-d913-4811-b205-ba4f31a31f03" />

---

1. File type.
2. Owner Permissions.
3. Group Permissions.
4. Other User Permission.
5. Link Count.
6. Owner of file/directory.
7. Group Owner of File or Directory.
8. File Size.
9. Creation Date and Time.
10. File/Directory Name.
---

- File Types in Linux: There are seven types of file available mentioned as below

<img width="858" height="211" alt="image" src="https://github.com/user-attachments/assets/61c05b5c-364b-4f7d-a351-ddf42e5ea72f" />

---
- Regular File: The regular file is a most common file type found on the Linux system. It governs all different files such us text files, images, binary files, shared libraries, etc.
- Directory: Directory is second most common file type found in Linux. Directory can be created with the mkdir command
- Character Device File: Character and block device files allow users and programs to communicate with hardware peripheral devices.
- Block Device File: Block devices are similar to character devices. They mostly govern hardware as hard drives, memory, etc.
- Local Domain Socket: Local domain sockets are used for communication between processes. Generally, they are used by services such as X windows, syslog and etc.
- Named piped: Similarly, as Local sockets, named pipes allow communication between two local processes. They can be created by the mknod command and removed with the rm command.
- Symbolic Link: With symbolic links an administrator can assign a file or directory multiple identities. Symbolic link can be thought of as a pointer to an original file.
---
### Link Count: Also called as reference count. It shows count of links of file/directory that has been created.
- Default link count of directory is 2 whereas default link count of file is 1. Whenever new directory is created, link count of its just parent directory will increase by 1.
There are two types of symbolic link
   - a. Hard Link
   - b. Soft Link
- Below is the difference between hard and soft links

<img width="856" height="407" alt="image" src="https://github.com/user-attachments/assets/2d76f5ab-e295-4f56-9fe0-b8166e725813" />

---
- Example
- Create Hardlink and softlink
```
[root@ip-172-31-19-5 ~]# ln /root/anaconda-ks.cfg /root/Documents/hardlink
[root@ip-172-31-19-5 ~]# ln –s /root/anaconda-ks.cfg /root/Documents/softlink
[root@ip-172-31-19-5 ~]# ll /root/Documents
Total 4
-rw-------. 2 root root 817 Nov 18 23:06 hardlink
lrwxrwxrwx. 1 root root 21 Dec 4 16:57 softlink -> /root/anaconda-ks.cfg
```
---
### User and group ownership:
  - Basically, by default, user who creates the file/directory is the owner and his primary group acquires group ownerships of that file/directory. User owner and group owner of file will be shown in 6th and 7th field as shown in the figure. “chown” command is use to change owner and group where as using “chgrp” we can change group ownership.
- Syntax
---
# chown <user_name>:<group_name> <file/dir_name> 
# chgrp <group_name> <file/dir_name>
---
- Example
- Change User Ownership

```
[root@cloudblitz ~]# touch samplefile.txt
[root@cloudblitz ~]# ll
-rw-r--r--. 1 root root 0 May 29 08:56 samplefile.txt
[root@cloudblitz ~]# chown chetan samplefile.txt
[root@cloudblitz ~]# ll
-rw-r--r--. 1 chetan root 0 May 29 08:57 samplefile.txt
```
---
- Change Group Ownership
```
[root@cloudblitz ~]# chgrp nagpur samplefile.txt
[root@cloudblitz ~]# ll
-rw-r--r--. 1 chetan nagpur 0 May 29 08:57 samplefile.txt
```
---
- Change user and group ownership using chown
```
[root@cloudblitz ~]# chown atul:TCS samplefile.txt
[root@cloudblitz ~]# ll
-rw-r--r--. 1 atul TCS  0 May 29 08:57 samplefile.txt
```
---
### Managing Permissions
  - Field 2nd, 3rd and 4th represents permissions for owner, group owner and other users. Each of that field contain three basic permissions which allow user to read, write, and executes files. The effect of these permissions differ when applied to file or directory. If applied to a file, the read permission gives user the right to open file for reading. Therefore, user can read it’s contain. “chmod” command is use to change these basic permissions.

<img width="857" height="278" alt="image" src="https://github.com/user-attachments/assets/740b9cd3-5216-4772-9716-95fdcf41cabc" />

---
- Change permission using letters
- Syntax
---
# chmod <u,g,o><+,-,=><r,w,x> <file_name>
---
<img width="856" height="103" alt="image" src="https://github.com/user-attachments/assets/518ddc0a-f8aa-465b-a53b-c652d1ecb619" />

---
- Example
- Give write permission to group
---
[root@ip-172-31-41-212 ~]# mkdir /nagpur 
[root@ip-172-31-41-212 ~]# chmod g+w /nagpur/ 
[root@ip-172-31-41-212 ~]# ls -ld /nagpur/ 
drwxrwxr-x. 2 root root 6 May 25 06:14 /nagpur/
---
---
- Remove read and write permission for other users
```
[root@ip-172-31-41-212 ~]# chmod o-rx /nagpur/
[root@ip-172-31-41-212 ~]# ls -ld /nagpur
drwxrwx---. 2 root root 6 May 25 06:14 /nagpur
```
---
- Assign read only permission for group and other users
```
[root@ip-172-31-41-212 ~]# chmod go=r /nagpur/
[root@ip-172-31-41-212 ~]# ls -ld /nagpur
drwxr--r--. 2 root root 6 May 25 06:14 /nagpur
```
--- 
- Give execute permission to owner of file
```
[root@cloudblitz ~]# touch samplefile3.txt
[root@cloudblitz ~]# chmod u+rwx samplefile3.txt
[root@cloudblitz ~]# ll
-rwxr--r--. 1 root root 0 May 29 09:29 samplefile3.txt
```
---
- Remove read permission for group and assign read and write permission to other users
```
[root@ip-172-31-41-212 ~]# chmod g-r,o=rw samplefile3.txt
[root@ip-172-31-41-212 ~]# ls –l samplefile3.txt
-rwx---rw-. 1 root root 0 May 29 09:29 samplefile3.txt
```
---
- Change permission using octal number
- Syntax
```
# chmod <permission_in_numbers> <file_name>
```
---

<img width="847" height="240" alt="image" src="https://github.com/user-attachments/assets/504910d9-979c-4256-8bea-71dc771a0ba6" />

---
- Example
- Changing permission using octal number
```
[root@ip-172-31-41-212 ~]# mkdir /abhi
[root@ip-172-31-41-212 ~]# chmod 421 /abhi/
[root@ip-172-31-41-212 ~]# ls -ld /abhi/
dr---w---x. 2 root root 6 May 25 07:10 /abhi/
```
---
```
[root@ip-172-31-41-212 ~]# chmod 732 /abhi/
[root@ip-172-31-41-212 ~]# ls -ld /abhi/
drwx-wx-w-. 2 root root 6 May 25 07:10 /abhi/
```
---
```
[root@ip-172-31-41-212 ~]# chmod 644 /abhi/
[root@ip-172-31-41-212 ~]# ls -ld /abhi/
drw-r--r--. 2 root root 6 May 25 07:10 /abhi/
```
---
```
[root@ip-172-31-41-212 ~]# chmod 755 /abhi/
[root@ip-172-31-41-212 ~]# ls -ld /abhi/
drwxr-xr-x. 2 root root 6 May 25 07:10 /abhi/
```
---
### Default Permission:
  - When a user creates a file as a regular user, it’s given permission rw- rw-r-- (664) by default. A directory is given the permission rwxrwxr-x (775). For the root user, file and directory permission are rw-r--r-- (644) and rwxr-xr-x (755), respectively. These default values are determined by the value of umask. Type umask to see what your umask value is.
If you ignore the leading zero for the moment, the umask value masks what is considered to be fully opened permissions for a file 666 or a directory 777. The umask value of 002 results in permission for a directory of 775 (rwxrwxr-x). That same umask results in a file permission of 644 (rw-rw-r--).

- Default Permission for root and standard user

<img width="857" height="77" alt="image" src="https://github.com/user-attachments/assets/bd51e81e-95d7-4b87-b349-88a833b8bc0d" />

---
- Calculating Permission with Umask
<img width="857" height="127" alt="image" src="https://github.com/user-attachments/assets/41a880d9-bf94-4085-ae25-0666ee627768" />

---
- Umask for root user and standard user
```
[root@cloudblitz ~]# umask                               -> default umask for root user
0022
[student@cloudblitz ~]$ umask                            -> umask for standard user
0002
```
---
- Changing umask value temporary
```
[root@cloudblitz ~]# umask 000
[root@cloudblitz ~]# mkdir demo
[root@cloudblitz ~]# ll
drwxrwxrwx. 2 root root 6 May 29 12:34 demo
```
---
- Changing umask value permanent

```
[root@cloudblitz ~]# vim /etc/profile
59 if [ $UID -gt 199 ] && [ "`/usr/bin/id -gn`" = "`/usr/bin/id -un`" ]; then
60 umask 002 #change value for standard user line 60
61 else
62 umask 000 #change the value for root line 62
63 fi
:wq
[root@cloudblitz ~]# source /etc/profile
[root@cloudblitz ~]# umask
0000
```
---
### Special Permission:
  - Special Permission: We have three types of special permission, i.e. suid, sgid, and stickey bit.

<img width="847" height="307" alt="image" src="https://github.com/user-attachments/assets/6114bb21-8f5d-4af8-91ed-d242e55092ed" />

---
### SUID (set user identity):
  - SUID (Set owner User ID up on execution) is a special type of file permissions given to a file. Normally in Linux/UNIX when a program runs, it inherits access permissions from the logged in user. SUID is defined as giving temporary permissions to a user to run a program/file with the permissions of the file owner rather that the user who runs it. In simple words users will get file owners permissions as well as owner UID and GID when executing a file/program/command.
  - Syntax
```
# chmod u+s <file_name>
```
---
- Example
- (As we seen in basic commands, dmidecode command is use to get hardware information of the system. But dmidecode command is owned by root user and present in /sbin directory. That means, no local user can access it. Following example illustrates this scenario, and then set suid permission on command. After applying suid permission, any user can execute this command.)
```
[shubham@ip-172-31-19-21 ~]$ dmidecode
# dmidecode 3.0
/sys/firmware/dmi/tables/smbios_entry_point: Permission denied
Scanning /dev/mem for entry point.
/dev/mem: Permission denied
[shubham@ip-172-31-19-21 ~]$ logout
[root@ip-172-31-19-21 ~]# which dmidecode
/sbin/dmidecode
[root@ip-172-31-19-21 ~]# ll /sbin/dmidecode
-rwxr-xr-x 1 root root 110608 Jul 31 2018 /sbin/dmidecode
[root@ip-172-31-19-21 ~]# chmod u+s /sbin/dmidecode
[root@ip-172-31-19-21 ~]# ll /sbin/dmidecode
-rwsr-xr-x 1 root root 110608 Jul 31 2018 /sbin/dmidecode
[root@ip-172-31-19-21 ~]# su - shubham
Last login: Thu Dec 12 05:38:58 UTC 2019 on pts/0
[shubham@ip-172-31-19-21 ~]$ dmidecode
# dmidecode 3.0
Getting SMBIOS data from sysfs.
SMBIOS 2.7 present.
11 structures occupying 359 bytes.
Table at 0x000EB01F.
Handle 0x0000, DMI type 0, 24 bytes
BIOS Information
Vendor: Xen
...
```
---
### SGID (set group identity):
  - SGID (Set Group ID up on execution) bit is set on directory if we give SGID permission to particular directory and if file created in that directory by root user or local user that files will get directory group ownership automatically. In other words, when we applied sgid bit to particular directory, it inherit group permission to all files and directories that will create in sgid applied directory.
  - Syntax
```
# chmod g+s <file_name>
```
---
- Example
```
[root@ip-172-31-19-21 ~]# mkdir /demo
[root@ip-172-31-19-21 ~]# chgrp TCS /demo
[root@ip-172-31-19-21 ~]# ll -d /demo
drwxr-xr-x 2 root TCS 6 Dec 12 05:55 /demo
[root@ip-172-31-19-21 ~]# touch /demo/file
[root@ip-172-31-19-21 ~]# ll /demo/file
-rw-r--r-- 1 root root 0 Dec 12 05:56 /demo/file
[root@ip-172-31-19-21 ~]# chmod g+s /demo
[root@ip-172-31-19-21 ~]# ll -d /demo
drwxr-sr-x 2 root shubham 31 Dec 12 05:57 /demo
[root@ip-172-31-19-21 ~]# touch /demo/file1
[root@ip-172-31-19-21 ~]# ll /demo
total 0
-rw-r--r-- 1 root root 0 Dec 12 05:56 file
-rw-r--r-- 1 root TCS 0 Dec 12 05:57 file1
```
---
### Stickey Bit:
  - Sticky Bit is mainly used on folders in order to avoid deletion of a folder and its content by other users though they having write permissions on the folder contents. If Sticky bit is enabled on a folder, the folder contents are deleted by only owner who created them and the root user. No one else can delete other user’s data in this folder (Where sticky bit is set). This is a security measure to avoid deletion of critical folders and their content (sub-folders and files), though other users have full permissions.
  - Syntax
```
# chmod o+t <file_name>
```
---
- Example
```
[root@ip-172-31-19-21 ~]# mkdir /demo
[root@ip-172-31-19-21 ~]# chmod 777 /demo
[root@ip-172-31-19-21 ~]# chmod o+t /demo
[root@ip-172-31-19-21 ~]# su - shubham
[shubham@ip-172-31-19-21 ~]$ touch /demo/file.txt
[shubham@ip-172-31-19-21 ~]$ logout
[root@ip-172-31-19-21 ~]# su - chetan
[chetan@ip-172-31-19-21 ~]$ rm –f /demo/file.txt
rm: cannot remove ‘/demo/file.txt’: Operation not permitted
```
---
## ACL (access control list):
 - ACL use to set permission over file and directory to specific user or specific group. We can assign multiple user with different permission on same file or directory. Access control list (ACL) provides an additional, more flexible permission mechanism for file systems. It is designed to assist with UNIX file permissions. ACL allows you to give permissions for any user or group to any disc resource.
 - Think of a scenario in which a particular user is not a member of group created by you but still you want to give some read or write access, how can you do it without making user a member of group, here comes in picture Access Control Lists, ACL helps us to do this trick. Basically, ACLs are used to make a flexible permission mechanism in Linux. From Linux man pages, ACLs are used to define more fine-grained discretionary access rights for files and directories.
 - setfacl and getfacl are used for setting up ACL and showing ACL respectively.
 - Syntax
```
# setfacl -m u:<user_name>:<permissions> <file_name>  for user
# setfacl –m g:<grp_name>:<permissions> <file_name>  for group
```
---
- Syntax
```
# getfacl <file_name>
```
---
- Examples
- For user perspective
```
[root@ip-172-31-19-21 ~]# mkdir /project
[root@ip-172-31-19-21 ~]# ll -d /project
drwxr-xr-x 2 root root 6 Dec 12 05:55 /project
[root@ip-172-31-19-21 ~]# useradd amit                                          -> other users
[root@ip-172-31-19-21 ~]# useradd sumit                                         -> other users
[root@ip-172-31-19-21 ~]# setfacl -m u:amit:rwx /project                        -> apply acl
[root@ip-172-31-19-21 ~]# getfacl /project                                      -> check acl
[root@ip-172-31-19-21 ~]# su - amit
[amit@ip-172-31-19-21 ~]$ touch /project/amit.txt                               -> successfully create
[amit@ip-172-31-19-21 ~]$ exit
[root@ip-172-31-19-21 ~]# setfacl -m u:sumit:r-- /project
[root@ip-172-31-19-21 ~]# su - sumit
[sumit@ip-172-31-19-21 ~]$ cd /project                                          -> permission denied
```
---
- For group perspective
```
[root@ip-172-31-19-21 ~]# groupadd TCS
[root@ip-172-31-19-21 ~]# groupadd WIPRO
[root@ip-172-31-19-21 ~]# useradd -G TCS T1
[root@ip-172-31-19-21 ~]# useradd -G TCS T2
[root@ip-172-31-19-21 ~]# useradd -G WIPRO W1
[root@ip-172-31-19-21 ~]# useradd -G WIPRO W2
[root@ip-172-31-19-21 ~]# useradd -G WIPRO W3
[root@ip-172-31-19-21 ~]# ll -ld /project
drwxr-xr-x 2 root root 6 Dec 12 05:55 /project
[root@ip-172-31-19-21 ~]# getfacl /project
[root@ip-172-31-19-21 ~]# setfacl -m g:TCS:rwx /project
[root@ip-172-31-19-21 ~]# setfacl -m g:WIPRO:--- /project
[root@ip-172-31-19-21 ~]# getfacl /project
[root@ip-172-31-19-21 ~]# setfacl –m u:w3:rwx /project
```
- In above example, we have no permission of group WIPRO but we can put some permission to the user ‘W3’ of WIPRO group.
---
- Copy ACL of file/dir to another file/dir
```
[root@ip-172-31-19-21 ~]# touch /abc.txt
[root@ip-172-31-19-21 ~]# getfacl /abc.txt
[root@ip-172-31-19-21 ~]# getfacl /project | setfacl --set-file=- /abc.txt
[root@ip-172-31-19-21 ~]# getfacl /abc.txt
```
---
- Remove ACL from file/dir
```
[root@ip-172-31-19-21 ~]# setfacl -x u:amit /project                                       -> removing single user
[root@ip-172-31-19-21 ~]# setfacl -x u:sumit,u:W3 /project                                 -> multi-user
[root@ip-172-31-19-21 ~]# setfacl -x g:IBM /project                                        -> removing single group
[root@ip-172-31-19-21 ~]# setfacl -x g:WIPRO,g:TCS /project                                -> multi-group
[root@ip-172-31-19-21 ~]# getfacl /project
[root@ip-172-31-19-21 ~]# setfacl -b /abc.txt                                              -> removing all ACL
```
---
## SUDO permission:
  - sudo (Super User DO) command in Linux is generally used as a prefix of some command that only superuser are allowed to run. If you prefix sudo with any command, it will run that command with elevated privileges or in other words allow a user with proper permissions to execute a command as another user, such as the superuser. This is the equivalent of “run as administrator” option in Windows. The option of sudo lets us have multiple administrators. To allow user to use sudo command, user must be listed in “/etc/sudoers” file. Or user should belong to wheel group. Wheel group is default group which allow users to use sudo command.
  - Syntax
```
# sudo <command_line>
```
---
- Examples
```
[root@ip-172-31-19-21 ~]# su – amit
[amit@ip-172-31-19-21 ~]$ useradd shubham
-bash: /usr/sbin/useradd: Permission denied
[amit@ip-172-31-19-21 ~]$ sudo useradd shubham
```
---







































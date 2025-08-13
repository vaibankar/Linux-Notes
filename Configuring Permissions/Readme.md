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






















































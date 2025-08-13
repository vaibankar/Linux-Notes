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
















































































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
-File Types in Linux: There are seven types of file available mentioned as below















































































# File Creation
## touch – Touch command is used to create files. Using touch command, multiple files can be created.
Syntax:
```
 touch <filename>
```
## Examples:
1.Creating file in current directory:
```
[root@server0 /]# touch file1.txt
```
2. Creating file in desired directory
```
[root@server0 /]# touch /root/file1.txt
```
---
3.Creating multiple file at different locations (below example will create two files, one at
/root/Desktop and 2nd at /etc directory. You can add more file names along with their path and separate them by space.)
```
[root@server0 /]# touch /root/Desktop/file1.txt /etc/data.mp3
```
4.Creating multiple files at same location but with different file names (below example will create 3 files. You can add more file names and separate them by coma)
```
[root@server0 /]# touch /root/{data.txt,file.txt,demo.mp3}
```
5.Creating multiple files having continuous number in their names (below example will create hundred files with name starting from file1 to file100.)
```
[root@server0 /]# touch /root/file{1..100}.txt
```
---




























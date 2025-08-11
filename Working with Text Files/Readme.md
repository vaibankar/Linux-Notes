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
2.Creating file in desired directory
```
[root@server0 /]# touch /root/file1.txt
```
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
## mkdir :- mkdir command creates directories. Creating multiple directories are also possible using mkdir command
Syntax: 
```
mkdir <option> <path/directory_name>
```
## Example:-
1.Creating directory in / directory
```
[root@server0 /]# mkdir /dir1
```
2.Creating multiple directories
```
[root@server0 /]# mkdir /dir1 /root/Desktop/dir2 /etc/demo
[root@server0 /]# mkdir /root/{demo,data,practice}
[root@server0 /]# mkdir /practical{1..10}
```
3.Creating parent directory if it is not exist
```
[root@server0 /]# mkdir –p /demo/data/practice
```
---
# File Operations:-
## READ:- Read operation can be performed to view content of the file. There are five commands which we can use for read operation.
- cat:- cat command is used to get data of file as output on the terminal. Reading out large file leads to navigate in terminal, which require separate scrolling      device (mouse). So, cat command is very useful in reading smaller files with few lines of data in command line.

- Example:-
```
[root@server0 /]# cat /root/anaconda-ks.cfg
```
- more – more command provides line by line navigation and page by page navigation in downward direction but, upward scrolling not possible.
- Example:-
```
[root@server0 /]# more /root/anaconda-ks.cfg
```
- less – less command allow navigation keys for scrolling up and down. Thus, it is more useful command than any other four command.
- Example:-
```
[root@server0 /]# less /root/anaconda-ks.cfg
```
- head – head command show few lines from top of the file. If head command is used without any option, it will show top ten lines by default. –n is used to give             count of lines to be shown.
- Example:-
```
[root@server0 /]# head /root/anaconda-ks.cfg
[root@server0 /]# head –n 5 /root/anaconda-ks.cfg
```
- tail – tail command show few lines from bottom of file. If tail command is used without any option, it will show bottom ten lines by default. –n is used to give            count of lines to be shown.
- Example:-
```
[root@server0 /]# tail /root/anaconda-ks.cfg
[root@server0 /]# tail –n 4 /root/anaconda-ks.cfg
```
---
## SORT: - Sort command will display result in ascending or descending order. Without option, data will be shown in ascending order.
- Options:
     - -r to show output in reverse order
     - -k <n> to show output of arranged by sorting nth column.
-Example:-
```
[root@server0 /]# sort file1.txt
[root@server0 /]# sort –r file1.txt
```
---
## COPY: - Copy operation use to copy files and directories in Linux, from one location to another. It will copy contents of one file to another. If destination file is not exist in given location then automatically new file will be generated.
- Syntax:
 ```
 cp <option> <source> <destination>
```
- Options:
  - -f : forcefully
  - -v : Verbose/View
  - -r : recursive (to copy directory)
  - -a : preserver permissions when copying

- Example:-
- Copy one file content to another file
```
[root@server0 /]# cp /root/anaconda-ks.cfg ~/Desktop/kickstart.txt
```
- Copy file from one location to another
```
[root@server0 /]# cp /root/anaconda-ks.cfg /mnt/              ->copy single file
```
- Copy directory and multiple files
```
[root@server0 /]# cp -r /etc /root                            ->copy directory etc
[root@server0 /]# cp –r /root/* /media                        ->copy all files from root
 [root@server0 /]# cp –rv /abc.txt /xyz.mp3 /media            ->copy multiple files
```
---
## MOVE AND RENAME: - Move and rename both operation can be performed using ‘mv’ command. It moves files and directories from one location to another. It is possible to move and rename at the same time.
- Syntax
```
mv <option> <source> <destination>
```
- Example:-
- Move files/directories from one location to another
```
[root@server0 /]# mv /root/anaconda-ks.cfg /mnt/             ->move single file
[root@server0 /]# mv /media ~/Desktop/                       ->move directory
[root@server0 /]# mv /root/* /mnt/                           ->move all files
```
- Rename file or directory
```
[root@server0 /]# mv fower flower.txt                        ->rename file
[root@server0 /]# mv /root/anaconda-ks.cfg /root/kickstart.cfg
[root@server0 /]# mv /opt /demo                              -> rename directory
```
- Move and rename together
```
[root@server0 /]# mv /root/anaconda-ks.cfg ~/Desktop/kickstart.txt
```
---
## REMOVE: - ‘rmdir’ command is use to remove empty directory where as ‘rm’ command is used to remove files. Directories also can be removed using ‘rm’ command. (Note: Removing files using rm or rmdir command will delete files permanently and doesn’t move in recyclebin or any other place.)
- #rmdir – rmdir command only deletes empty directories.
- Syntax
```
#rmdir <empty_dir_name>
```
- Examples:-
- Trying to remove non-empty directory using rmdir. It gives error.
```
[root@server0 ~]# rmdir /Demo
rmdir: failed to remove ‘/Demo’: Directory not empty
```
- Removing empty directory using rmdir
```
[root@server0 ~]# rmdir /Demo/data
```
## rm – rm command is use to delete files and directories. 
- Syntax
```
#rm <option> <file_names>
```
- Examples:-
- Removing files
```
[root@server0 ~]# rm /Demo/file10.txt
rm: remove regular file ‘/Demo/file10.txt’? y
```
- Remove files without interaction, (-f : forcefully, -v : verbosely)
```
[root@server0 ~]# rm -vf /Demo/file1.txt
removed ‘/Demo/file1.txt’
```
- Remove all files
```
[root@server0 ~]# rm –f /Demo/*
```
- Remove directories, (-r : recursive)
```
[root@server0 ~]# rm –r /Demo
```
---
# Redirectors:
- Redirectors are used to write terminal output into file. Output, generated from any command, on terminal can be transferred into existing file. If file does not exist, automatically new file will be created. Following are some redirectors.
## Single Redirector (>): Single redirector replace existing data in the file with newly redirected data. It overwrites the contents of existing file.
## Double Redirector (>>): Double redirector keeps existing data and newly redirected data will be added at the end of the file. It appends redirected data in existing file.






















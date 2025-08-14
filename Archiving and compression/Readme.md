- Archiving is the process of combining multiple files and directories (same or different sizes) into one file. On the other hand, compression is the process of reducing the size of a file or directory. Archiving is usually used as part of a system backup or when moving data from one system to another. One of the oldest and most common command for creating and working with backup archive `tar` command. With `tar` users can gather large amount of data into single unit known as archive.

- Syntax:
```
tar <-options> <compress_fileName>.tar <files_to_be_compressed>
```
---
  - -c -> create an archive.
  - -f -> file name. (Compulsory option)
  - -v -> verbose or view.
  - -t -> list the content from archive.
  - -x -> execute the content from archive.
  - -P -> preserve permission when extracting file or directory.
  - -C -> copy content from an archive to another directory.

- Examples
- Archive file using tar command
```
[root@localhost ~]# du –sh /etc                                  -> disk usage or size of file/dir
34M              /etc
[root@localhost ~]# tar -cvf /backup.tar /etc
tar: Removing leading  `/'  from member names
/etc/
/etc/netconfig
/etc/dracut.conf.d/
/etc/egl/
/etc/egl/egl_external_platform.d/
/etc/rc4.d
...
[root@localhost ~]# du –sh /backup.tar
30M      /backup.tar
```
---
- Listing archive file
```
[root@localhost ~]# tar -tvf /backup.tar
drwxr-xr-x root/root      0 2018-09-15 16:13 etc/
-rw-r--r-- root/root      767 2018-08-28 01:51 etc/netconfig
drwxr-xr-x root/root      0 2018-07-30 11:07 etc/dracut.conf.d/
drwxr-xr-x root/root      0 2018-09-02 22:17 etc/egl/
...
```
- Extraction of archived files
```
[root@localhost ~]# tar –xvf /backup.tar                                -> extract at current directory
...
[root@localhost ~]# tar –xvf /backup.tar –C /demo/                      -> extract at different
... location
[root@localhost ~]# du –sh /demo/etc
34M       /demo/etc
```
---

### Compression using gzip, bzip2, and xz

- Compression is a reduction in the number of bits needed to represent data.
Compressing data can save storage capacity, speed up file transfer, and decrease costs for storage hardware and network bandwidth.

- `GZIP`: GZIP is good option for compressing a lot of data as it is quick. Its memory usage is also low. GZIP compression can be used by using `“-z”` option in `tar` command or by using `gzip` command. GZIP compressed file can be extracted using `gunzip`.

- `BZIP2`: BZIP2 provide better compression ratio compared to GZIP but require more "CPU time" to accomplish it. `“-j”` option in tar or `bzip2` command can be used for bzip2 compression. Bunzip2 is command to extract bzip2 compressed file.

- `XZ`: XZ use LZMA algorithm which provide impressive compression ration but in cost of very high CPU and Memory usage. Decompression speed is better but it also consumes a lot of memory. XZ compression can be done by `“-J”` option in tar or xz command.
---
- METHODS OF AN ARCHIVE
<img width="856" height="100" alt="image" src="https://github.com/user-attachments/assets/faca26cf-f3dc-411a-b83a-810876f42508" />

---
- Examples
- Compression using `tar` command

```
[root@localhost ~]# du –sh /etc
34M      /etc
[root@localhost ~]# tar –czvf /backup1.tar.gz /etc                        -> using gzip method
[root@localhost ~]# du –sh /backup1.tar.gz
8.4M      /backup1.tar.gz
[root@localhost ~]# tar –cjvf /backup2.tar.bz2 /etc                       -> using bzip2 method
[root@localhost ~]# du –sh /backup2.tar.bz2
7.0M     /backup2.tar.bz2
[root@localhost ~]# tar –cJvf /backup3.tar.xz /etc                        -> using xz method
[root@localhost ~]# du –sh /backup3.tar.xz
5.7M     /etc.tar.xz
```
---
- Extraction using `tar` command
```
[root@localhost ~]# mkdir /gz_xtr /bz2_xtr /xz_xtr                             -> create dir for extraction
[root@localhost ~]# tar –xvzf /backup1.tar.gz –C /gz_xtr                       -> for gzip
[root@localhost ~]# ls /gz_xtr
etc
[root@localhost ~]# tar –xvjf /packup2.tar.bz2 –C /bz2_xtr                     -> for bzip2
[root@localhost ~]# ls /bz2_xtr
etc
[root@localhost ~]# tar –xvJf /packup3.tar.xz –C /xz_xtr                      -> for xz
[root@localhost ~]# ls /xz_xtr
etc
```
---
- Compression using `gzip` command
```
[root@localhost ~]# du –sh /etc
34M     /etc
[root@localhost ~]# tar -cvf /etc.tar /etc
[root@localhost ~]# ls /
etc.tar
[root@localhost ~]# du -sh /etc.tar
30M  /etc.tar
[root@localhost ~]# gzip /etc.tar
[root@localhost ~]# ls /
etc.tar.gz
[root@localhost ~]# du -sh /etc.tar.gz
8.4M   /etc.tar.gz
```
---
- When we use gzip command for compression, the original archive file get compressed and replaced with new compressed file. This helps you to avoid unnecessary wasting of storage space for both original file and compressed file. Also, new compressed file will get .gz extension automatically. You can clearly see in it above example. Similarly, bzip2 and xz commands also generates compressed file and replace the old file.

- Compression using bzip2 command
```
[root@localhost ~]# tar -cvf /etc.tar /etc
[root@localhost ~]# ls /
etc.tar
[root@localhost ~]# du -sh /etc.tar
30M  /etc.tar
[root@localhost ~]# bzip2 /etc.tar
[root@localhost ~]# ls /
etc.tar.bz2
[root@localhost ~]# du -sh /etc.tar.bz2
7.5M  /etc.tar.bz2
```
---
- Compression using xz command
```
[root@localhost ~]# tar -cvf /etc.tar /etc
[root@localhost ~]# ls /
etc.tar
[root@localhost ~]# du -sh /etc.tar
30M  /etc.tar
[root@localhost ~]# xz /etc.tar
[root@localhost ~]# ls /
etc.tar.xz
[root@localhost ~]# du -sh /etc.tar.xz
5.8M  /etc.tar.xz
```
---
- Extraction using `gunzip`, `bunzip2`, and `unxz` command 
- `gunzip`, `bunzip2`, and `unxz` commands are used to extract the respective type of compressed files. It replaces the compressed files with new extracted files and also removes extension of compressing method.
```
[root@localhost ~]# gunzip /etc.tar.gz
[root@localhost ~]# bunzip2 /etc.tar.bz2
[root@localhost ~]# unxz /etc.tar.bz2
```
--- 
### Search and Filter utility in Linux

- Search utilities are used to search files from the system where as filter utilities filters the output.
- Following are some filter tools that can we use
  - `cat` – displays the text from file as output
























































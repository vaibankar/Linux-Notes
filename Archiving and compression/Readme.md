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


























































































- For everything that happens on a Linux server, a process is started. For that reason, process management is among the key skills that an administrator has to master. To do this efficiently, it is important to know which type of process you are dealing with.
- A major distinction can be made between two process types:
  - Shell jobs are commands started from the command line. They are associated with the shell that was current when the process was started. Shell jobs are also referred to as interactive processes.
  - Daemons are processes that provide services. They normally are started when a computer is booted and often (but certainly not in all cases) they are running with root privileges.
### Running Jobs in the Foreground and Background
- Command Use
<img width="855" height="361" alt="image" src="https://github.com/user-attachments/assets/01c486dd-f167-4505-92f5-150c74ef24c3" />

---
### Understanding Processes and Threads
  - Tasks on Linux are typically started as processes. One process can start several worker threads. Working with threads makes sense, because if the process is very busy, the threads can be handled by different CPUs or CPU cores available in the machine. As a Linux administrator, you cannot manage individual threads; you can manage processes, though. It is the programmer of the multithreaded application that has to define how threads relate to one another.
  - ps command and some of its important options

<img width="856" height="122" alt="image" src="https://github.com/user-attachments/assets/e2599c20-9dee-44c1-b868-95955f05cea0" />

---
- Monitoring processes using ps fax
```
[root@server2 ~]# ps fax
PID TTY STAT TIME COMMAND
1603 ? Ss 0:00 /usr/sbin/sshd -D
35395 ? Ss 0:00 \_ sshd: root@pts/1
```
---
- Monitoring processes using ps aux
```
[root@server1 /]# ps aux
USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND
root 1 0.0 0.4 52984 4272 ? Ss Feb05 0:03 /usr/lib/
systemd/systemd --switched-root --system --deserialize 23
root 2 0.0 0.0 0 0 ? S Feb05 0:00 [kthreadd]
root 3 0.0 0.0 0 0 ? S Feb05 0:00 [ksoftirqd/0]
root 5 0.0 0.0 0 0 ? S< Feb05 0:00 [kworker/0:0H]
root 7 0.0 0.0 0 0 ? S Feb05 0:00 [migration/0]
root 8 0.0 0.0 0 0 ? S Feb05 0:00 [rcu_bh]
root 9 0.0 0.0 0 0 ? S Feb05 0:00 [rcuob/0]
...
```
---
- Monitoring processes using ps –ef
```
[root@server2 ~]# ps -ef
UID PID PPID C STIME TTY TIME CMD
root 874 1 0 May14 ? 00:00:00 /sbin/auditd -n
root 885 874 0 May14 ? 00:00:00 /sbin/audispd
root 889 885 0 May14 ? 00:00:00 /usr/sbin/sedispatch
root 898 1 0 May14 ? 00:00:00 /usr/sbin/alsactl -s -n
19 -c -E ALSA_CONFIG_PATH=/etc/alsa/alsactl.conf --initfile=/lib/alsa/
root 899 1 0 May14 ? 00:00:00 /usr/sbin/bluetoothd -n
libstor+ 903 1 0 May14 ? 00:00:00 /usr/bin/lsmd -d
root 905 1 0 May14 ? 00:02:14 /usr/bin/vmtoolsd
root 908 1 0 May14 ? 00:00:00 /usr/sbin/rsyslogd -n
root 910 1 0 May14 ? 00:00:00 /usr/sbin/abrtd -d -s
...
```
---
- Important columns of ps command’s output
<img width="856" height="313" alt="image" src="https://github.com/user-attachments/assets/9aaf15a3-61a9-494c-b165-8a51ed0f85ff" />

---
### Adjusting Process Priority with nice 
  - When Linux processes are started, they are started with a specific priority. By default, all regular processes are equal and are started with the same priority, which is the priority number 20. In some cases, it is useful to change the default priority that was assigned to the process when it was started. You can do that using the nice and renice commands. Changing process priority may make sense in two different scenarios.
  - Example: that you are about to start a backup job that does not necessarily have to finish fast. Typically, backup jobs are rather resource intensive, so you might want to start it in a way that it is not annoying other users too much, by lowering its priority.
  - Another example is where you are about to start a very important calculation job. To ensure that it is handled as fast as possible, you might want to give it an increased priority, taking away CPU time from other processes. When using nice or renice to adjust process priority, you can select from values ranging from -20 to 19.
  - Changing nice value using renice command
```
[root@server2 ~]# sleep 1000 & [2] 2261
[root@server2 ~]# ps –l
F S UID   PID   PPID C PRI NI   ADDR SZ WCHAN TTY TIME CMD
4 S 0     2061  2054 0 80  0    - 29065 wait pts/0 00:00:00 bash
0 S 0     2261  2061 0 80  0    - 26973 hrtime pts/0 00:00:00 sleep
0 R 0     2387  2061 0 80  0    - 30315 - pts/0 00:00:00 ps
[root@server2 ~]# renice -n -10 -p 2261
[root@server2 ~]# ps –l
F S UID   PID   PPID C PRI NI   ADDR SZ WCHAN TTY TIME CMD
4 S 0     2061  2054 0 80   0   - 29065 wait pts/0 00:00:00 bash
0 S 0     2261  2061 0 70  -10  - 26973 hrtime pts/0 00:00:00 sleep
```
---
`Note`= TIP: Do not set process priority to -20; it risks blocking other processes from getting served.

---
###m Sending Signals to Processes with kill, killall, and pkill
- The Linux kernel allows many signals to be sent to processes. Use man 7 signals for a complete overview of all the available signals. Three of these signals work for all processes:
   - The signal SIGTERM (15) is used to ask a process to stop.



















































































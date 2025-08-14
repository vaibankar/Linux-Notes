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
   - The signal SIGKILL (9) is used to force a pr-ocess to stop.
   - The SIGHUP (1) signal is used to hang up a process. The effect is that the process will reread its configuration files, which makes this a useful signal to use after making modifications to a process configuration file.

- To send a signal to a process, the kill command is used. The most common use is the need to stop a process, which you can do by using the kill command followed by the PID of the process. This sends the SIGTERM signal to the process, which normally causes the process to cease its activity.

- Sometimes the kill command does not work because the process you want to kill is busy. In that case, you can use kill -9 to send the SIGKILL signal to the process.

- Because the SIGKILL signal cannot be ignored, it forces the process to stop, but you also risk losing data while using this command. In general, it is a bad idea to use kill -9 because
   
    - You risk losing data.
    - Your system may become unstable if other processes depend on the process you have just killed.

- Sending signal using kill command
```
[root@server2 ~]# kill –l
1) SIGHUP 2) SIGINT 3) SIGQUIT 4) SIGKILL 5) SIGTRAP
6) SIGABRT 3) SIGBUS 8) SIGFPE 9) SIGKILL 10) SIGUSR1
...
[root@server2 ~]# kill -9 2261
```
---
`Note`= TIP: Use kill -l to show a list of available signals that can be used with kill.

---
### Linux Process States Overview

<img width="856" height="377" alt="image" src="https://github.com/user-attachments/assets/ad23b1db-4cde-47c1-bb1a-5671c7f25c60" />

---
### Monitoring process using top command

  - top command is used to show the Linux processes. It provides dynamic real-time view of running system. Usually, this command shows the summary information of the system and the list of processes or threads which are currently managed by the Linux Kernel. As soon as you will run this command it will open an interactive command mode where the half portion will contain the statistics of processes and resource usage. And Lower half contains a list of the currently running processes. Pressing q will simply exit the command mode.

```
[root@server2 ~]# top
top - 02:19:11 up 4 days, 10:37, 5 users, load average: 0.07, 0.13, 0.09
Tasks: 160 total, 1 running, 159 sleeping, 0 stopped, 0 zombie
Cpu(s): 10.7%us, 1.0%sy, 0.0%ni, 88.3%id, 0.0%wa, 0.0%hi, 0.0%si, 0.0%st
Mem: 760752k total, 644360k used, 116392k free, 3988k buffers
Swap: 1540088k total, 76648k used, 1463440k free, 196832k cached

PID    USER      PR   NI   VIRT   RES   SHR   S   %CPU   %MEM   TIME+     COMMAND
14401  jhradile  20   0    313m   10m   5732  S   5.6    1.4    6:27.29   gnome-system-mo
1764   root      20   0    133m   23m   4756  S   5.3    3.2    6:32.66   Xorg
13865  jhradile  20   0    1625m  177m  6628  S   0.7    23.8    0:57.26  java
20     root      20   0     0      0     0    S   0.3    0.0    4:44.39   ata/0
2085   root      20   0    40396  348   276   S   0.3    0.0    1:57.13   udisks-daemon
1      root      20   0    19404  832   604   S   0.0    0.1    0:01.21   init
2      root      20   0     0      0     0    S   0.0    0.0    0:00.01   kthreadd
3      root      RT   0     0      0     0    S   0.0    0.0    0:00.00   migration/0
4      root      20   0     0      0     0    S   0.0    0.0    0:00.02   ksoftirqd/0
5      root      RT   0     0      0     0    S   0.0    0.0    0:00.00   migration/0
6      root      RT   0     0      0     0    S   0.0    0.0    0:00.00   watchdog/0
Controlling
```
---
## Controlling Jobs

- A job is a process that the shell manages. Each job is assigned a sequential job ID. Because a job is a process, each job has an associated PID. There are three types of job statuses:

   - Foreground: When you enter a command in a terminal window, the command occupies that terminal window until it completes. This is a foreground job.
   - Background: When you enter an ampersand (&) symbol at the end of a command line, the command runs without occupying the terminal window. The shell prompt is displayed immediately after you press Return. This is an example of a background job.
   - Stopped: If you press Control + Z for a foreground job, or enter the stop command for a background job, the job stops. This job is called a stopped job.

- Example
- Running job in background
```
[root@localhost ~]# sleep 200 &
 [2] 2261
[root@localhost ~]# jobs                              --> listing jobs
[1]- Running               sleep 1000 &
[2]+ Running               sleep 200 &
```
---
- Bring background jobs to foreground
```
[root@localhost ~]# fg %1
sleep 1000
^Z                                                -> used ctrl+z to stop foreground process
[1]+ Stopped(SIGTSTP) sleep 1000
```
---
## Killing Processes

Usually, a process terminates on its own when they’re done with their task, or when you ask them to quit. However, sometimes a process can hang up or consume a lot of CPU or RAM. In this situation, you would want to manually “kill” the process. In order to kill a process, you should first locate the details of the process. You can do this through following commands: `top`, `ps`, `pidof` and `pgrep`.

- (We had already seen how to get details of processes using top and ps command in this chapter.) Getting process details using pgrep,

- `pgrep` command searches for processes currently running on the system, based on a complete or partial process name, or other specified attributes.

```
[root@localhost ~]# pgrep -a sleep                            -> all processes of name ‘sleep’
2261 sleep 1000
2368 sleep 200
[root@localhost ~]# pgrep -a -u root                          -> all processes of root user
1 /bin/sh /sbin/init
2 kthreadd
3 kworker/0:0
4 kworker/0:0H
5 kworker/u2:0
6 mm_percpu_wq
...
2261 sleep 1000
2368 sleep 200
```
---
- Getting process details using pidof

- `pidof` command searches processes currently running on system. This command is similar to pgrep command but it shows process id only.
```
[root@localhost ~]# pidof sleep
2261 2368
```
---
- Getting process details using pstree and pidstat

- `pstree` command is similar to ps command but instead of showing detailed information, pstree command shows processes in tree structure. Pstree command followed by user name will give process tree generated from that particular user.

- `pidstat` command is used for monitoring individual tasks currently being managed by the Linux kernel. It writes to standard output activities for every task managed by the Linux kernel. The pidstat command can also be used for monitoring the child processes of selected tasks. The interval parameter specifies the amount of time in seconds between each report.

- Important signals that are used to kill or terminate the process:
<img width="855" height="135" alt="image" src="https://github.com/user-attachments/assets/e19547fb-2845-4368-8445-dc16eb806952" />

---
- Examples
- Killing process using process id

```
[root@localhost ~]# pgrep –a sleep
2261 sleep 1000
2368 sleep 200
[root@localhost ~]# kill -9 2261
[1]+ Killed       sleep 1000
```
---

- Killing process using process name (using pkill or killall)
```
[root@localhost ~]# pgrep –a sleep
2261 sleep 1000
2368 sleep 200
[root@localhost ~]# killall sleep
[1]- Terminated       sleep 1000
[2]+ Terminated       sleep 200
```
---
- System Information using `uptime`

- Uptime tell how long the system has been running. It gives a one line display of the following information. The current time, how long the system has been running, how many users are currently logged on, and the system load averages for the past 1, 5, and 15 minutes.

```
[root@localhost ~]# uptime
14:39:12 up 1:17, 2 users,        load average: 0.00, 0.05, 0.05
```
---




























































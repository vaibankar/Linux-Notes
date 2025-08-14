- Job scheduling is a feature that allows a user to submit a command or program for execution at a specified time in the future. On a Linux server, it is important that certain tasks run at certain times the execution of the command or program could be one time or periodically based on a pre- determined time schedule. For example, scheduling system maintenance commands to run during nonworking hours is a good practice, as it does not disrupt normal business activities.
- In Linux, we have three methods to schedule a job

   - at – single time execution
   - crontab – periodic execution
   -  anacron – periodic execution
---
# at
   - The at command uses atd service for executing jobs. At command queued the task
into /var/spool/at and executes them when it is scheduled. After execution, tasks removed from the queue. After writing desired jobs, you can save jobs using shortcut key `“ctrl+d”`
- Syntax
```
# at “<time> <date>”
```
---
- Example
- Scheduling at job
```
[root@localhost ~]# at “14:30 31 jan 2020”
at> touch /root/file.txt
at> mkdir /root/Practice
at> <EOT>
job 3 at Fri Jan 31 14:30:00 2020
```
---
- Query for queued tasks
```
[root@localhost ~]# atq
2   Thu Feb 14 10:00:00 2020 a root
3   Fri Jan 31 14:30:00 2020 a root
```
---
- Removing queued jobs
```
[root@localhost ~]# atrm 2
[root@localhost ~]# atq
3   Fri Jan 31 14:30:00 2020 a root
```
---
# crontab

   - Crontab is similar as that of window task scheduler in windows. In Linux, we schedule jobs using `crontab`. Crontab job scheduling technique is very useful for creating backup, scanning system, performing jobs with daily, weekly, monthly basis, etc. A daemon called crond runs in the background and check its configuration every minute to examine configuration files in order to execute commands or shell scripts specified in the crontab if the time matches with specified time. Crontab can executes job repeatedly in specified time interval.

   - Crond executes cron jobs on a regular basis if they comply with the format defined in the `/etc/crontab` file. Crontables for users are located in the `/var/spool/cron` directory. A cron table includes six fields separated by space or tab characters. The first five fields specify the times to run the command, and the sixth field is the absolute pathname to the command to be executed. These fields are mentioned in /etc/crontab file.

- /etc/crontab file

```
# cat /etc/crontab
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root

# For details see man 4 crontabs # Example of job definition:

# .---------------- minute (0 - 59)
# | .------------- hour (0 - 23)
# | | .---------- day of month (1 - 31)
# | | | .------- month (1 - 12) OR jan,feb,mar,apr ...
# | | | | .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,...
# | | | | |
# * * * * * user-name command to be executed
```
---
- Syntax
```
# crontab <option>
```
---
- Options

  - -e = Edit cron table
  - -l = List cron table
  - -r = Remove crontable
  - -u = Specify user
  - -e –u = Edit crontable for specific user
  - -l –u = List crontable of specific user
  - -r –u = Remove crontable of specific user
---
- Example
- Suppose, we have to schedule following jobs

  1. Create a file in /root/Downloads dir with name FLOWER.txt at 10.30 pm on 15 Aug.
  2. Display “Welcome to Cloudblitz” massage on terminal at midnight of every Saturday.
  3. Display “HELLO” massage on terminal after every hour on 10th of Jan, Feb, and March

```
[root@localhost ~]# crontab –e                                        -> editing current user’s crontab
30 22 15 aug * /bin/touch /root/Downloads/FLOWER.txt
0 0 * * sat /bin/echo “Welcome to Irise”
0 * 10 jan,feb,mar * /bin/echo “HELLO”
```
---
-  Listing crontable
```
[root@localhost ~]# crontab –l
30 22 15 aug * /bin/touch /root/Downloads/FLOWER.txt
0 0 * * sat /bin/echo “Welcome to Irise”
0 * 10 jan,feb,mar * /bin/echo “HELLO”
```
---
- Scheduling a job for Natasha user, creating file in Natasha’s home directory at 10 am on Jan 31st.

```
[root@localhost ~]# crontab –e –u natasha
0 10 31 jan * /bin/touch ~/demo
```
---





























































































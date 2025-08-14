# Understanding System Logging
 - Most services used on a Linux server write information to log files. This information can be written to different destinations, and there are multiple solutions to find the relevant information in system logs. No less than three different approaches can be used by services to write log information:
    
    - `direct write`: Some services write logging information directly to the log files, even some important services such as the Apache web server and the Samba file server.
    - `rsyslogd`: rsyslogd is the enhancement of syslogd, a service that takes care of managing centralized log files. Syslogd has been around for a long time.
    - `journald`: With the introduction of systemd to the journald log service, systemd-journald service has been introduced. This service is tightly integrated with systemd, which allows administrators to read detailed information from the journal while monitoring service status using the systemctl status command.

---
# Understanding the Role of rsyslogd and journald

- On RHEL 7, journald (which is implemented by the systemd-journald daemon) provides an advanced log management system. journald collects messages from the kernel, the entire boot procedure, and services and writes these messages to an event journal. This event journal is stored in a binary format, and it can be queried using the journalctl command.

- Because the journal that is written by journald is not persistent between reboots, messages are also forwarded to the rsyslogd service. Rsyslogd writes the messages to different files in the
/var/log directory. rsyslogd also offers features that do not exist in journald, such as centralized logging and filtering messages by using modules.

- In the current state of Red Hat Enterprise Linux 7, journald is not a replacement for rsyslog; it is just another way of logging information.

- Using `systemctl` Status to Show Relevant Log Information

```
[root@ip-172-31-24-16 ~]# systemctl status sshd
● sshd.service - OpenSSH server daemon
  Loaded: loaded (/usr/lib/systemd/system/sshd.service; enabled; vendor
preset: enabled)
  Active: active (running) since Thu 2020-01-30 04:38:47 UTC; 2min 5s ago
  Docs: man:sshd(8)
        man:sshd_config(5)
Main PID: 3367 (sshd)
  CGroup: /system.slice/sshd.service
          └─3367 /usr/sbin/sshd -D

Jan 30 04:38:47 ip-172-31-24-16.us-east-2.compute.internal systemd[1]:Starting Op...
Jan 30 04:38:47 ip-172-31-24-16.us-east-2.compute.internal sshd[3367]: Server list...
Jan 30 04:38:47 ip-172-31-24-16.us-east-2.compute.internal sshd[3367]: Server list...
Jan 30 04:38:47 ip-172-31-24-16.us-east-2.compute.internal systemd[1]: Started
```
---
## Reading Log Files

- Apart from the messages that are written by journald to the journal, and which can be read using the
`journalctl` command, on a Linux system you’ll also find different log files in the directory /var/log.


<img width="857" height="496" alt="image" src="https://github.com/user-attachments/assets/78fbdcff-4051-4124-b8f2-ee0b9c397b77" />

---
## Understanding Log File Contents

- Example, (message logs)
```
[root@ip-172-31-24-16 ~]# tail -5 /var/log/messages
Jan 30 04:43:47 ip-172-31-24-16 amazon-ssm-agent: </body>
Jan 30 04:43:47 ip-172-31-24-16 amazon-ssm-agent: </html>
Jan 30 04:45:08 ip-172-31-24-16 dhclient[3012]: XMT: Solicit on eth0, interval
131720ms.
Jan 30 04:47:19 ip-172-31-24-16 dhclient[3012]: XMT: Solicit on eth0, interval
114430ms.
Jan 30 04:49:14 ip-172-31-24-16 dhclient[3012]: XMT: Solicit on eth0, interval
114820ms.
```
---
- `Date and time`: Every log message starts with a timestamp. For filtering purposes.
- `Host`: The host the message originated from. This is relevant because rsyslogd can be configured to handle remote logging as well.
- `Service or process name`: The name of the service or process that generated the message.
- `Message content`: The content of the message, which contains the exact message that has been logged.
---

- Live Log File Monitoring
- Syntax
```
# tail –f <logfile>
```
---
- Example
```
[root@ip-172-31-24-16 ~]# tail -f /var/log/messages
Jan 30 04:47:19 ip-172-31-24-16 dhclient[3012]: XMT: Solicit on eth0, interval
114430ms.
Jan 30 04:49:14 ip-172-31-24-16 dhclient[3012]: XMT: Solicit on eth0, interval
114820ms.
Jan 30 04:50:01 ip-172-31-24-16 systemd: Created slice User Slice of root.
Jan 30 04:50:01 ip-172-31-24-16 systemd: Starting User Slice of root.
Jan 30 04:50:01 ip-172-31-24-16 systemd: Started Session 3 of user root.
Jan 30 04:50:01 ip-172-31-24-16 systemd: Starting Session 3 of user root.
Jan 30 04:50:01 ip-172-31-24-16 systemd: Removed slice User Slice of root.
Jan 30 04:50:01 ip-172-31-24-16 systemd: Stopping User Slice of root.
```
---
- Using logger
- Most services write information to the log files all by themselves. The logger command enables users
to write messages to rsyslog from the command line. User can write logs manually.
- Syntax
```
# logger <option> <Message>
```
---
- Example, (Writing log with priority option,)
```
[root@ip-172-31-24-16 ~]# logger –p local3.err “Danger”
[root@ip-172-31-32-167 ~]# tail -3 /var/log/messages
Jan 30 06:10:41 ip-172-31-32-167 systemd-logind: New session 5 of user ec2-user.
Jan 30 06:10:41 ip-172-31-32-167 systemd: Starting Session 5 of user ec2-user.
Jan 30 06:11:14 ip-172-31-32-167 ec2-user: Danger
```
---
## Configuring rsyslogd

- To make sure that the information that needs to be logged is written to the location where you want to find it, you can configure the rsyslogd service through the /etc/rsyslog.conf file.

  ### **Understanding rsyslogd Configuration Files**
   
      - Like many other services on RHEL 7, the configuration for rsyslogd is not defined in just one configuration file. The /etc/rsyslogd.conf file is the central location where rsyslogd is
configured. From this file, the content of the directory /etc/rsyslog.d is included. This directory can be populated by installing RPM packages on a server. When looking for specific log
configuration, make sure to always consider the contents of this directory also.
 
      - If specific options need to be passed to the rsyslogd service on startup, you can do
this by using the /etc/sysconfig/rsyslog file. This file by default contains one line, which reads
SYSLOGD_OPTIONS. On this line, you can specify rsyslogd startup parameters. The
SYSLOGD_OPTIONS variable is included in the systemd configuration file that starts rsyslogd.
Theoretically, you could change startup parameters in this file, as well, but that is not
recommended

   - **Understanding rsyslog.conf Sections**

  - The rsyslog.conf file is used to specify what should be logged and where it should be
logged. To do this, you’ll find different sections in the configuration file:

  - #### MODULES ####: rsyslogd is modular. Modules are included to enhance the
supported features in rsyslogd.

  - #### GLOBAL DIRECTIVES ####: This section is used to specify global parameters,
such as the location where auxiliary files are written or the default timestamp format.

  - #### RULES ####: This is the most important part of the rsyslog.conf file. It
contains the rules that specify what information should be logged to which destination. 

**Understanding Facilities, Priorities, and Log Destinations** 
























































































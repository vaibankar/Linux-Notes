# Understanding System Logging
 - Most services used on a Linux server write information to log files. This information can be written to different destinations, and there are multiple solutions to find the relevant information in system logs. No less than three different approaches can be used by services to write log information:
    
    - direct write: Some services write logging information directly to the log files, even some important services such as the Apache web server and the Samba file server.
    - rsyslogd: rsyslogd is the enhancement of syslogd, a service that takes care of managing centralized log files. Syslogd has been around for a long time.
    - journald: With the introduction of systemd to the journald log service, systemd-journald service has been introduced. This service is tightly integrated with systemd, which allows administrators to read detailed information from the journal while monitoring service status using the systemctl status command.

---
# Understanding the Role of rsyslogd and journald

- On RHEL 7, journald (which is implemented by the systemd-journald daemon) provides an advanced log management system. journald collects messages from the kernel, the entire boot procedure, and services and writes these messages to an event journal. This event journal is stored in a binary format, and it can be queried using the journalctl command.

- Because the journal that is written by journald is not persistent between reboots, messages are also forwarded to the rsyslogd service. Rsyslogd writes the messages to different files in the
/var/log directory. rsyslogd also offers features that do not exist in journald, such as centralized logging and filtering messages by using modules.

- In the current state of Red Hat Enterprise Linux 7, journald is not a replacement for rsyslog; it is just another way of logging information.

- Using systemctl Status to Show Relevant Log Information

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






















































































































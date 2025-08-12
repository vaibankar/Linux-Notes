### A user is a person who utilizes a computer or network service. Linux is said to be secure because one user cannot access files of other user without its permission.
- There are three types of user.
1. Super user: Super users are those users who has all privileges of Linux system. On all Linux systems, by default there is the user root, also known as the super user. This account is used for managing Linux. Root, for instance, can create other user accounts on the system. For some tasks, root privileges are required. Some examples are installing software, managing users, and creating partitions on disk devices.
2. System user: System accounts are used by the services in Linux system. These accounts or users generally created when services are installed in system.
3. Standard user: local user accounts or standard user accounts are for the people who need to work on a system and who need limited access to the resources on that system. These user accounts typically have a password that is used for authenticating the user to the system.
---
### Adding New User
```
[root@ip-172-31-19-5 ~]# useradd shubham
```
- Adding new local user means creating user account. User can be added by root user or using root user’s privileges. Whenever new user has been added, some files get affected. These files holds user accounts related information. Also whenever new user is created, by default, its home directory and mail account also has been generated. New users are created using some skeleton files located in
/etc/skel directory. These files are hidden and copied into home directory of new user.
---
### Files affected by newly added user
 - /etc/passwd: It store user profile related information
```
[root@ip-172-31-19-5 ~]# tail -1 /etc/passwd
shubham:x:1002:1002::/home/shubham/:/bin/bash
```
---
- /etc/shadow: It stores user password policies
```
[root@ip-172-31-19-5 ~]# tail -1 /etc/shadow
shubham:!!:18206:0:99999:7:::
```
---
- /etc/group: It store group information
```
[root@ip-172-31-19-5 ~]# tail -1 /etc/group
shubham:x:1002:
```
---
- /etc/gshadow: Stores group password and member’s list
```
[root@ip-172-31-19-5 ~]# tail -1 /etc/gshadow
shubham:!::
```
---
### Home directory and Mail account of new user
```
[root@ip-172-31-19-5 ~]# ls /home
centos shubham                                          -> Home directories
[root@ip-172-31-19-5 ~]# ls /var/spool/mail/
centos rpc shubham                                      -> Mail Accounts
```
## Skeleton files
   - .bash_logout: if this file is missing, user will unable to logout from the system.
   - .bash_profile: If this file is missing, home directory will not be assigned to the new user.
   - .bashrc: If this file is missing, user will unable to login to the system.
```
[root@ip-172-31-19-5 ~]# ls -a /etc/skel                                   -> skeleton files
. .. .bash_logout .bash_profile .bashrc
[root@ip-172-31-19-5 ~]# ls -a /home/shubham                               -> skeleton that copied in
. .. .bash_logout .bash_profile .bashrc                                    home directory
```
---
### Switching between users
-  su: The ‘su’ command is use to switch user. It allows user to open a sub shell with different logged in user. Switching user from root to other local user will not require any password. But, switching from        local user to any other user will require password of that user for authentication and login.
## Syntax,
```
# su - <user_name>
````
### Example:-
- Switching from root user to local user (shubham)
```
[root@ip-172-31-19-5 centos]# su - shubham
Last login: Wed Nov 6 11:53:05 UTC 2019 on pts/0
[shubham@ip-172-31-19-5 ~]$
```
---
- Switching from local user (shubham) to any other user (centos)
```
[shubham@ip-172-31-19-5 ~]$ su - centos
Password:
Last login: Wed Nov 6 11:52:19 UTC 2019 from 49.36.29.134 on pts/0
[centos@ip-172-31-19-5 ~]$
```
  - (Note: Switching user using ‘su’ command will open new sub shell with different user login. But, previous user remains logged in. You have to logout user manually.)
---
### Password Management
- passwd: Password is the secret phrase that can be used to login to the system. ‘passwd’ command will be used to assign or change password of any user by root user. Whenever, password assigned to the user, it will stored in /etc/shadow file in encrypted format. Only root user can change password of any user, but local users can change their own password. Password should follow some rules such as,

    - Password must be 8 character long
    - It should not contain user name
    - It cannot accept old password
    - Any dictionary name is not allowed
    - Password should not be too simplistic

 - Syntax
   ```
   #passwd                                       -> change current user’s password
   #passwd <user_name>                           -> assign or change other user’s password by root user
   ```

### Example
- Changing root user’s password
```
[root@ip-172-31-19-5 ~]# passwd
Changing password for user root.
New password:
BAD PASSWORD: The password is shorter than 8 characters
Retype new password:
passwd: all authentication tokens updated successfully.
```





























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
---
- Changing local user’s password by root user’s account
```
[root@ip-172-31-19-5 centos]# passwd shubham
Changing password for user shubham.
New password:
BAD PASSWORD: The password is shorter than 8 characters
Retype new password:
passwd: all authentication tokens updated successfully.
```
---
- Changing current user’s password (local user changing its own password)
```
[shubham@ip-172-31-19-5 ~]$ passwd
Changing password for user shubham.
Changing password for shubham.
(current) UNIX password:
New password:
Retype new password:
passwd: all authentication tokens updated successfully.
```
---
- Changing other user’s password by local user’s account, (it generates error because only root user has privilege to change other user’s password)
```
[shubham@ip-172-31-19-5 ~]$ passwd centos
passwd: Only root can specify a user name.
```
---
- Password are stored in /etc/shadow file in encrypted format
```
[root@ip-172-31-19-5 ~]# tail -1 /etc/shadow
shubham:$6$S59rUkc4$iIusUTs6TPb2ueLMty3/2kvShejrTVctesfLYyUwTa78kDQQ/O/f954Euy
omO6nBwwiPyqPt4hAij5OxiQIQ5.:18206:0:99999:7:::
```
---
- /etc/shadow file: /etc/shadow file stores password and password policies of all users. It contains nine fields and each field is separated by colon. Below is the summary of these fields
```
[root@ip-172-31-19-5 ~]# tail -1 /etc/shadow
shubham:$6$S59rUkc4$iIusUTs6TPb2ueLMty3/2kvShejrTVctesfLYyUwTa78kDQQ/O/f954Euy
omO6nBwwiPyqPt4hAij5OxiQIQ5.:18206:0:99999:7:::
```
---
①:②:③:④:⑤:⑥:⑦:⑧:⑨
1. Username: This is a unique name for the user. User names are important to match a user to his password. On Linux, there can be no spaces in the user name.
2. Encrypted password: This field contains all that is needed to store the password in a secure way.
3. Days since Jan 1, 1970, that the password was last changed: Many things on Linux refer to this date, which on Linux is considered the beginning of days.
4. Days before password may be changed: This is minimum age of password. That means user cannot change password, before the mentioned days, after immediately changing the password. Typically this field is set to the value 0.
5. Days after which password must be changed: This field contains the maximal validity period of passwords or maximum age of password. User must have to change their password after mentioned days. By default it is set to 99999 days.
6. Days before password is to expire that user is warned: This field is used to warn a user when a forced password change is upcoming. By default it is set to 7 days.
7. Days after password expires that account is disabled: Use this field to enforce a password change. After password expiry, users can no longer log in.
8. Days since Jan 1, 1970, that account is disabled: An administrator can set this field to disable an account. This is typically a better approach than removing an account, as all associated properties and files of the account will be kept, but it can be used no longer to authenticate on your server.
9. For future use: This is reserved field for future use.
---
- View and change password policy
  - #chage – ‘chage’ (change age) command use to view or modify password policy of user.
- Syntax
```
# chage <option> <parameter> <username>
```
- Options
  - -l = list / view password policy.
  - -m = min. days between password change.
  - -M = maximum days between password change.
  - -W = number of days of warning.
  - -I = number of inactivation days.
  - -E = Expiry date of user account.
  - -d = force to change password.
---
- Example
- View password policies
```
[root@ip-172-31-37-64 ]# chage -l amit
Last password change                                 : May 25, 2019
Password expires                                     : never
Password inactive                                    : never
Account expires                                      : never
Minimum number of days between password change       : 0
Maximum number of days between password change       : 99999
Number of days of warning before password expires    : 7
```
---
- Change minimum age
```
[root@ip-172-31-37-64 ]# chage -m 30 amit
[amit@ip-172-31-37-64 ~]$ chage -l amit
Last password change                                  : May 25, 2019
Password expires                                      : never
Password inactive                                     : never
Account expires                                       : never
Minimum number of days between password change        : 30
Maximum number of days between password change        : 99999
Number of days of warning before password expires     : 7
```
---
- Change maximum age
```
[root@ip-172-31-37-64 ]# chage -M 45 amit
[amit@ip-172-31-37-64 ~]$ chage -l amit
Last password change                                 : May 25, 2019
Password expires                                     : Jul 09, 2019
Password inactive                                    : never
Account expires                                      : never
Minimum number of days between password change       : 30
Maximum number of days between password change       : 45
Number of days of warning before password expires    : 7
```
---
- Change warning days
```
[root@ip-172-31-37-64 ]# chage -W 0 amit
[amit@ip-172-31-37-64 ~]$ chage -l amit
Last password change                                  : May 25, 2019
Password expires                                      : Jul 09, 2019
Password inactive                                     : never
Account expires                                       : never
Minimum number of days between password change        : 30
Maximum number of days between password change        : 45
Number of days of warning before password expires     : 0
```
---
- Change expiry date of user account
```
[root@ip-172-31-37-64 ]# chage -E "20 OCT 2018" amit
[root@ip-172-31-37-64 ]# su - amit
[amit@ip-172-31-37-64 ~]$ chage -l amit
Last password change                                   : May 25, 2019
Password expires                                       : Jul 09, 2019
Password inactive                                      : never
Account expires                                        : Oct 20, 2018
Minimum number of days between password change         : 30
Maximum number of days between password change         : 45
Number of days of warning before password expires      : 0
```
---
- Change password immediately
```
[root@ip-172-31-37-64 amit]# chage -d 0 amit
[amit@ip-172-31-37-64 ~]$ chage -l amit
Last password change                                  : password must be changed
Password expires                                      : password must be changed
Password inactive                                     : password must be changed
Account expires                                       : Oct 20, 2018
Minimum number of days between password change        : 30
Maximum number of days between password change        : 45
Number of days of warning before password expires     : 0
```
---
## Group Administration/Management
  - Linux users can be a member of two different kinds of groups. First, there is the primary group. Every user must be a member of a primary group and there is only one primary group. When creating files, the primary group becomes group owner of these files.
Users can also access all files their primary group has access to. The user’s primary group membership is defined in /etc/passwd; the group itself is stored in the /etc/group configuration file. Besides the mandatory primary group, users can be a member of one or more secondary groups as well. Secondary groups are important to get access to files. If the group a user is a member of has access to specific files, the user will get access to these files also.

### groupadd – ‘groupadd’ command is use to add secondary or supplementary group in system. Group information are stored in /etc/group file.
- Syntax
```
# groupadd <groupname>
```
- Example
```
[root@ip-172-31-37-64 ~]# groupadd IBM
[root@ip-172-31-37-64 ~]# tail -1 /etc/group
IBM:x:1005:
```
---
### /etc/group file: This file contain all group’s information. The file has four fields and each field is separated by colon (:). Following are fields of shadow file
①:②:③:④
1. Group name: As is suggested by the name of the field, this contains the name of the group.
2. Redirected group password: A feature that is hardly used anymore. A group password can be used by users that want to join the group on a temporary basis, so that access to files the group has access to is allowed.
3. Group id (GID): A unique numeric group identification number.
4. List of members: Here you find the names of users that are a member of this group as a secondary group. Note that it does not show users that are a member of this group as their primary group.
---
- Adding group with customize setting
- Syntax
```
# groupadd <option> <parameter> <groupname>
```
- Options
  - -g = Group id
  - -o = Non unique
  - -f = Forcefully

- Example
```
[root@ip-172-31-37-64 ~]# groupadd -g 2005 TCS
[root@ip-172-31-37-64 ~]# tail -1 /etc/group
TCS:x:2005:
```
---
- Modify existing group with customize setting
- Syntax
```
# groupmod <option> <parameter> <groupname>
```
- Options
  - -g = Group id
  - -n = Group Name
  - -o = Non unique
- Example
- Change group id of existing group
```
[root@ip-172-31-37-64 ~]#groupmod -g 5903 IBM
[root@ip-172-31-37-64 ~]# tail -1 /etc/group
IBM:x:5903:
```
---
- Changing group name of existing group
```
[root@ip-172-31-37-64 ~]# groupmod -n TATA TCS
[root@ip-172-31-37-64 ~]# tail -2 /etc/group
TATA:x:2005:
```
---
## User Administration/Management
- useradd – `useradd` command use to create new user account.
- Syntax
```
# useradd <username>
```
- Example
```
[root@ip-172-31-19-5 ~]# useradd shubham
```
---
- /etc/passwd file: This file stores user profile information. It contain 7 fields as follows

①:②:③:④:⑤:⑥:⑦
1. User login name: This is a unique name for the user. User names are important to match a user to his password, which is stored separately in /etc/shadow. On Linux, there can be no spaces in the user name.
2. Password link from shadow file: since /etc/passdw file is readable by all user, for security purpose, the password is stored in /etc/shadow file.
3. User id (UID): Each user has a unique user ID (UID). This is a numeric ID. It is the UID that really determines what a user can do. When permissions are set for a user, the UID is stored in the file metadata (and not the user name). UID 0 is reserved for root. The lower UIDs (typically up to 999) are used for system accounts, and the higher UIDs (from 1000 on by default), are reserved for people that need to connect directory to the server.
-  [Note:-/etc/login.defs contain default setting for user creation.]
4. Primary group’s id (GID): On Linux, each user is a member of at least one group. This group is referred to as the primary
5. Comment field: The Comment field, as you can guess, is used to add comments for user accounts. This field is optional, but it can be used to describe what a user account is created for.
6. Home Directory Home Directory: This is the initial directory where the user is placed after logging in, also referred to as the home directory. If the user account is used by a person, this is where the person would store his personal files and programs.
7. Login shell: This is the program that is started after the user has successfully connected to a server. For most users this will be / bin/bash, the default Linux shell. For system user accounts, it will typically be a shell like /sbin/nologin. The /sbin/nologin command is a specific command that silently denies access to users.
---
- Adding user with customized setting
- Syntax
```
# useradd <options> <parameters> <username>
```
- Options
   - -u = User id
   - -g = Primary group
   - -c = Comment
   - -d = Home directory
   - -s = Login shell
   - -G = Secondary group
   - -r = System user
   - -e = Account expiry date
   - -o = Non unique
---
- Example
- Create user with customized user id
```
[root@ip-172-31-19-5 ~]# useradd -u 2211 amit
[root@ip-172-31-19-5 ~]# tail -1 /etc/passwd
amit:x:2211:2211::/home/amit:/bin/bash
```
- Create user with comment
```
[root@ip-172-31-19-5 ~]# useradd -c "linux user" amit
[root@ip-172-31-19-5 ~]# tail -1 /etc/passwd
amit:x:2212:2212:linux user:/home/amit:/bin/bash
```
- Create user with customized home directory
```
[root@ip-172-31-19-5 ~]# useradd -d /project suresh
[root@ip-172-31-19-5 ~]# tail -1 /etc/passwd
suresh:x:2213:2213::/project:/bin/bash
```
- Create user with nologin shell
```
[root@ip-172-31-19-5 ~]# useradd -s /sbin/nologin mahesh
[root@ip-172-31-19-5 ~]# tail -1 /etc/passwd
mahesh:x:2214:2214::/home/mahesh:/sbin/nologin
```
- Create user with customized primary group
```
[root@ip-172-31-19-5 ~]# useradd -g IBM amit
[root@ip-172-31-19-5 ~]# tail -1 /etc/passwd
amit:x:2216:1003::/home/amit:/bin/bash
```
- Create user and assign secondary group
```
[root@ip-172-31-19-5 ~]# useradd -G IBM shubham
[root@ip-172-31-19-5 ~]# tail -2 /etc/group
IBM:x:1003:shubham
shubham:x:2216:
```
- Add user along with its expiry date
```
[root@ip-172-31-19-5 ~]# useradd -e "10 dec 2019" suresh
[root@ip-172-31-19-5 ~]# chage -l suresh
Last password change                                  : Nov 08, 2019
Password expires                                      : never
Password inactive                                     : never
Account expires                                       : Dec 10, 2019
Minimum number of days between password change        : 0
Maximum number of days between password change        : 99999
Number of days of warning before password expires     : 7
```
---
- Create user with multiple customize options
```
[root@ip-172-31-19-5 ~]# useradd -u 6001 -g TCS -G IBM -c "admin account" -d
/admin -s /bin/bash -e "31 dec 2030" shubham
[root@ip-172-31-19-5 ~]# tail -1 /etc/passwd
shubham:x:6001:1006:admin account:/admin:/bin/bash
[root@ip-172-31-19-5 ~]# tail -2 /etc/group
IBM:x:1003:shubham
TCS:x:1006:
[root@ip-172-31-19-5 ~]# chage -l shubham
Last password change                                   : Nov 08, 2019
Password expires                                       : never
Password inactive                                      : never
Account expires                                        : Dec 31, 2030
Minimum number of days between password change         : 0
Maximum number of days between password change         : 99999
Number of days of warning before password expires      : 7
```
---
### Modify user with customized setting
- #usermod – ‘usermod’ command is use to modify existing user’s setting.
- Syntax
```
# usermod <option> <parameters> <username>
```
- Options
   - -u = user id
   - -g = primary group
   - -c = Comment
   - -d = home directory
   - -s = login shell
   - -G = secondary group
   - -l = login name
   - -L = lock user password
   - -U = unlock user password
   - -m = modify directories
 ---
 -Example
 -Change user id
```
[root@ip-172-31-37-64 ~]# #usermod -u 7766 sumit
[root@ip-172-31-37-64 ~]# tail -1 /etc/passwd
sumit:x:6021:6021::/home/sumit:/bin/bash
```
---
- Change comment
```
[root@ip-172-31-37-64 ~]# usermod -c “windows” sumit
[root@ip-172-31-37-64 ~]# tail -1 /etc/passwd
sumit:x:6021:6021:windows:/home/sumit:/bin/bash
```
---
- Change home directory
```
[root@ip-172-31-37-64 ~]# usermod -m -d /home/namit sumit
[root@ip-172-31-37-64 ~]# tail -1 /etc/passwd
sumit:x:6021:6021:windows:/home/namit:/bin/bash
```
---
- Change login shell
```
[root@ip-172-31-37-64 ~]# usermod -s /bin/bash sumit
[root@ip-172-31-37-64 ~]# tail -1 /etc/passwd
sumit:x:6021:6021:windows:/home/namit:/bin/bash
```
---
- Assign secondary or supplementary group
```
[root@ip-172-31-37-64 ~]#usermod -G TCS suresh
[root@ip-172-31-37-64 ~]# tail -1 /etc/group
TCS:x:6023:suresh
```
---
- Change user login name
```
[root@ip-172-31-37-64 ~]# usermod -l sammuel ritesh
[root@ip-172-31-37-64 ~]# tail -1 /etc/passwd
sammuel:x:2214:2214::/home/ritesh:/bin/bash
```
---
- Change expiry date of account
```
[root@ip-172-31-37-64 ~]# usermod -e '14 dec 2018' ritesh
[root@ip-172-31-37-64 ~]# chage -l ritesh
Last password change                                   : May 25, 2019
Password expires                                       : never
Password inactive                                      : never
Account expires                                        : Dec 14, 2018
Minimum number of days between password change         : 0
Maximum number of days between password change         : 99999
Number of days of warning before password expires      : 7
```
---
- Lock and Unlock User Password
```
[root@ip-172-31-19-5 ~]# tail -1 /etc/shadow
amit:$6$lblryj7X$jDt1EWzSANqKVrW/KS4VSEBU/GTFFgUmfCNZJxBjV4kTUJWgirNaNKsHIg79Y
gUIPXO.VT50vQuNnu4ik64ZM/:18209:0:99999:7:::
[root@ip-172-31-19-5 ~]#
[root@ip-172-31-19-5 ~]# usermod -L amit  Lock Password
[root@ip-172-31-19-5 ~]# tail -1 /etc/shadow
amit:!$6$lblryj7X$jDt1EWzSANqKVrW/KS4VSEBU/GTFFgUmfCNZJxBjV4kTUJWgirNaNKsHIg79
YgUIPXO.VT50vQuNnu4ik64ZM/:18209:0:99999:7:::
[root@ip-172-31-19-5 ~]#
[root@ip-172-31-19-5 ~]# usermod -U amit  Unlock Password
[root@ip-172-31-19-5 ~]# tail -1 /etc/shadow
amit:$6$lblryj7X$jDt1EWzSANqKVrW/KS4VSEBU/GTFFgUmfCNZJxBjV4kTUJWgirNaNKsHIg79Y
gUIPXO.VT50vQuNnu4ik64ZM/:18209:0:99999:7:::
```
---
## Remove user from system
### #userdel – ‘userdel’ command is used to remove or delete user account from system.
- Syntax
```
# userdel <username>
```
- Example
- Delete user account
```
[root@ip-172-31-19-5 ~]# userdel amit
```
---
- Delete user account along with its home directory and mail account
```
[root@ip-172-31-19-5 ~]# userdel -r shubham
```
---

















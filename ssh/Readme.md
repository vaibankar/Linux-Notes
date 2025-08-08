📘 Table of Contents
Introduction to SSH

Installing SSH

Starting and Enabling SSH Service

Basic SSH Usage

SSH Key-based Authentication

SSH Configuration Files

Advanced SSH Commands

Securing SSH Server

Common SSH Errors and Fixes

Practical Exercises

1. 📌 Introduction to SSH
SSH (Secure Shell) is a protocol used to securely connect to remote machines over a network.

Default port: 22

Replaces: telnet, rlogin, FTP (in many cases)

2. 🔧 Installing SSH
🖥️ On Ubuntu/Debian:
bash
Copy
Edit
sudo apt update
sudo apt install openssh-server
🖥️ On CentOS/RHEL:
bash
Copy
Edit
sudo yum install openssh-server
🖥️ On Fedora:
bash
Copy
Edit
sudo dnf install openssh-server
3. ▶️ Starting and Enabling SSH Service
bash
Copy
Edit
# Start SSH service
sudo systemctl start ssh

# Enable SSH to start on boot
sudo systemctl enable ssh

# Check SSH status
sudo systemctl status ssh
For CentOS/RedHat, the service name might be sshd.

4. 💻 Basic SSH Usage
➤ Connect to a remote machine:
bash
Copy
Edit
ssh username@hostname_or_ip
Example:

bash
Copy
Edit
ssh user@192.168.1.10
➤ Specify a different port:
bash
Copy
Edit
ssh -p 2222 user@host
5. 🔑 SSH Key-based Authentication
➤ Generate SSH keys:
bash
Copy
Edit
ssh-keygen
Default location: ~/.ssh/id_rsa and ~/.ssh/id_rsa.pub

➤ Copy public key to remote host:
bash
Copy
Edit
ssh-copy-id user@remote_host
Manual method:

bash
Copy
Edit
cat ~/.ssh/id_rsa.pub | ssh user@remote_host "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"
➤ Connect without password:
bash
Copy
Edit
ssh user@remote_host
6. ⚙️ SSH Configuration Files
➤ User Config File:
bash
Copy
Edit
~/.ssh/config
Example:

ini
Copy
Edit
Host myserver
    HostName 192.168.1.10
    User ubuntu
    Port 2222
    IdentityFile ~/.ssh/id_rsa
Usage:

bash
Copy
Edit
ssh myserver
7. 🚀 Advanced SSH Commands
➤ SSH with port forwarding:
bash
Copy
Edit
ssh -L local_port:destination_host:destination_port user@ssh_server
Example (forward web server port):

bash
Copy
Edit
ssh -L 8080:localhost:80 user@remote_host
➤ Remote command execution:
bash
Copy
Edit
ssh user@host "ls -l /var/www"
➤ SCP (Secure Copy):
bash
Copy
Edit
scp file.txt user@remote_host:/path/to/destination
scp user@remote_host:/file.txt /local/path
➤ SFTP:
bash
Copy
Edit
sftp user@remote_host
8. 🛡️ Securing SSH Server
➤ Change default port:
Edit /etc/ssh/sshd_config:

yaml
Copy
Edit
Port 2222
➤ Disable root login:
nginx
Copy
Edit
PermitRootLogin no
➤ Allow specific users:
nginx
Copy
Edit
AllowUsers user1 user2
➤ Restart SSH service:
bash
Copy
Edit
sudo systemctl restart ssh
9. 🧩 Common SSH Errors and Fixes
Error	Fix
Connection refused	SSH service not running or wrong port
Permission denied (publickey)	Key not set or permissions wrong
Host key verification failed	Remove old key: ssh-keygen -R host
Too many authentication failures	Limit identities: ssh -o IdentitiesOnly=yes ...

10. 🛠️ Practical Exercises
✅ Install and start SSH on two Linux machines

✅ Connect to remote machine using SSH

✅ Set up key-based authentication

✅ Change SSH port and test

✅ Secure SSH using configuration best practices

✅ Use SCP to transfer files

✅ Create and use ~/.ssh/config for custom shortcuts

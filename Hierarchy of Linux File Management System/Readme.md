# 🐧 Linux File System Hierarchy

The Linux File System follows a hierarchical directory structure, starting from the root `/` directory. Each directory and subdirectory has a specific purpose and plays a vital role in system operation.

---

## 📂 Root Directory `/`

The root directory is the top-level directory in Linux. All other directories are its children.

/
├── bin/
├── boot/
├── dev/
├── etc/
├── home/
├── lib/
├── media/
├── mnt/
├── opt/
├── proc/
├── root/
├── run/
├── sbin/
├── srv/
├── sys/
├── tmp/
├── usr/
└── var/


---

## 📁 `/bin` - Essential User Binaries

- Contains essential user commands (binaries) required for system booting and repair.
- Examples: `ls`, `cp`, `mv`, `rm`, `bash`

---

## 📁 `/boot` - Boot Loader Files

- Contains all files needed for booting the system.
- Includes Linux kernel (`vmlinuz`), `initrd`, and bootloader config files like `grub.cfg`.

---

## 📁 `/dev` - Device Files

- Contains special files representing devices (hardware).
- Examples: `/dev/sda` (disk), `/dev/null`, `/dev/tty`

---

## 📁 `/etc` - System Configuration Files

- Contains configuration files for the system and installed applications.
- Examples: `/etc/passwd`, `/etc/fstab`, `/etc/hosts`, `/etc/ssh/`

---

## 📁 `/home` - User Home Directories

- Contains personal directories for each user.
- Example: `/home/alice`, `/home/bob`
- Each user's documents, downloads, and settings are stored here.

---

## 📁 `/lib` - Essential Shared Libraries

- Contains shared library files required by binaries in `/bin` and `/sbin`.

---

## 📁 `/media` - Removable Media

- Mount point for external devices such as USB drives, CDs.
- Example: `/media/usb`, `/media/cdrom`

---

## 📁 `/mnt` - Temporary Mount Point

- Used for mounting filesystems temporarily.
- Example: Manual mount targets like `/mnt/mydrive`

---

## 📁 `/opt` - Optional Software

- Contains third-party or optional software packages.
- Example: `/opt/google/`, `/opt/zoom/`

---

## 📁 `/proc` - Process and Kernel Information

- Virtual filesystem that provides information about running processes and kernel.
- Example: `/proc/cpuinfo`, `/proc/meminfo`, `/proc/[pid]/`

---

## 📁 `/root` - Root User's Home Directory

- Home directory of the `root` (superuser).
- Not to be confused with `/` (root directory of file system).

---

## 📁 `/run` - Runtime Variable Data

- Contains runtime information since the last boot.
- Replaces older `/var/run`.

---

## 📁 `/sbin` - System Binaries

- Contains essential system binaries used for system maintenance.
- Examples: `fsck`, `reboot`, `ifconfig`

---

## 📁 `/srv` - Service Data

- Contains service-related data provided by the system.
- Example: web or FTP service data.

---

## 📁 `/sys` - System Information

- Virtual filesystem similar to `/proc`.
- Interfaces with the Linux kernel and hardware devices.

---

## 📁 `/tmp` - Temporary Files

- Stores temporary files created by users and applications.
- Automatically cleared on reboot.

---

## 📁 `/usr` - User Utilities and Applications

- Contains user programs and data (larger, secondary hierarchy).











































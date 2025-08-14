# Software Management in Linux:

- In Linux, software is available in the form of packages (packages are the collection of programs). And installing the packages means simply extracting the files from the archive and put it on the system. Package Management is the method of installing and maintaining the software.
- Some package requires shared library, or another package, called dependency. Since there are many families of Linux, different distribution family use a different packaging system.
- Following are some commonly used package systems:
    - Red Hat Packages (*.rpm)
    - Debian Packages (*.deb)
    - Ubuntu Packages (*.pkg)
- There are two types of utilities we can use, low-level tool and high-level tool. Low-level tool manages package files installation, update and uninstallation whereas high-level tool can install the package with their dependencies.
<img width="853" height="147" alt="image" src="https://github.com/user-attachments/assets/9f734d56-d4b8-4ef3-bcc4-da407f2c3961" />

---
- `#rpm`: rpm is a RedHat Package Manager use to install package files on RedHat Linux system. It only install the package and not the dependency. It requires full pathname of package for installation.
```
#rpm <option> <package-name>
```
---
- Syntax:
- Options:

  - -i install package file
  - -v verbose
  - -h show hash bar
  - -U Upgrade package
  - -q query package
  - -e erase package

- Example:
- Installing Package from /package directory
```
#rpm –ivh /package/tree-1.6.0-10.e17.x86_64.rpm
```
---
- Updating Package from remote server
```
#rpm –Uvh http://classroom.com/content/tree-4.6.7-17.e17.x86_64.rpm
```
---
- [`Note`: Use complete pathname of package before installation. Use only service name of package after installation.]
- Query of package
```
#rpm –q tree                                                          -> shows the complete name
#rpm –qi tree                                                         -> installed package info
#rpm –qip /package/tree-4.6.7-17.e17.x86_64.rpm                       -> not-installed package info #rpm –qa -list all installed packages
#rpm –ql tree                                                         -> list of file extracted location
#rpm –qc tree                                                         -> list of configuration files
#rpm –qd tree                                                         -> list of documentation files
```
---
- Erase or uninstall the package
```
#rpm –evh tree
```
---
- `#yum`: yum is an open source CLI as well as GUI tool for rpm based system. It allow user to easily install, update, remove or search packages on system. Yum uses numerous third party repositories to install package automatically. This can also resolves the dependency issue. Yum does not require complete path-name of package for installation.
- Because yum uses repositories to get the packages, either you should keep repositories on your system or you should have access to the remote repositories. Repository is nothing but the meta- data of all the packages. Sometimes the packages are not get installed since, its repository is not available. In such case you can create your own repository or you can install the package using rpm but if you use rpm, all the dependencies should be installed manually.

- Syntax:
```
#yum <option/action> <package-name> [<-y/-d/-n>]
```
---
- Actions:
<img width="856" height="323" alt="image" src="https://github.com/user-attachments/assets/7655593e-eea2-4f44-b271-7150e3b1bb74" />

---
- Creating own repository:

- STEP1: install required packages for creating repository if it is not already installed.
```
#rpm –ivh createrepo
#rpm –ivh deltarpm
```
---
- STEP2: create metadata file of all packages
```
#createrepo –v /Packages
```
---
- STEP3: create new repository file into default repository path i.e. /etc/yum.repo.d/
```
#vim /etc/yum.repo.d/clientdemo.repo

[exampleID]                             ------> repo ID
name=Sampledemo                         ------> repo name
baseurl=file:///Packages                ------> url of packages(http:// or ftp:// for remote url)
enabled=1                                ------> 1 for enable, 0 for disable the
```
---
- STEP4: check repository
```
#yum repolist
#yum clean all                    ------> to clean yum cache
```
---
- Examples:
- Install httpd package
```
#yum install httpd
#yum install tree –y                   ---->  install without
```
---
- Install group of packages
```
#yum grouplist                      ----> list all groups
#yum groupinstall “Basic Web Server”
```
---
- Update all packages
```
#yum update –y
#yum update –y --exclude kernel       ----> update all but not
kernel packages
```
---
- Show package of specific command or service
```
#yum provide “nmcli”
```
---
- Other yum commands
```
#yum-config-manager –add-repo file:///Project                  ---> to create repository in shortcut way
```
---























































































































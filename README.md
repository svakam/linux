# Linux

Linux reference

## Acknowledgments

Jason Cannon: Professional system admin, consultant, author

## TOC
1. [Intro](#what-is-linux)
1. [Reasons to Use Linux](#why-linux)
1. [Defining a Linux distro](#linux-distro)
1. [Install Linux](#install-linux)
1. [Log into Linux and SSH](#getting-connected-log-into-linux-ssh)
1. [Common Directories](#common-directories)
1. [Linux Shell](#linux-shell)
1. [Basic Linux Commands](#basic-linux-commands)
1. [Working With Directories](#working-with-directories)
1. [Listing Files and Understanding LS Output](#listing-files-and-understanding-ls-output)

## What is Linux?
An operating system (OS), which is a collection of software that manages hardware resources and provides an environment to run applications. Allows applications to store information, send documents to printers, interact with users, and more. 

The term "Linux" most commonly refers to the Linux OS, but it also refers to the kernel. This is the core of the operating system and is the intermediary between hardware and software. Additional components are needed to supplement the kernel, like system libraries, etc. 

Linux is FOSS (Free/Open Source Software). 

## Why Linux?

Linux runs on multiple hardware platforms (phones, networking devices, PCs, supercomputers), while proprietary UNIX systems only run on specified hardware. 

It has a small footprint, which makes it compatible with older hardware. 

It works great for servers, since it's stable, reliable and secure; but it can also be used as a desktop. 

It's FOSS. 

## Linux Distro
A Linux distro, or distribution, is the Linux kernel + additional software like applications to create the full operating system. The software that comes installed by default can be removed and/or replaced. 

There are hundreds of distributions, each with a different focus, and many distributions are available to choose from and use depending on the need. 

Distributions can be commercial or non-commercial, for server use, for desktop use, for research, for multimedia, and others. Examples include Red Hat Enterprise Linux (RHEL), Fedora, Ubuntu, Debian, SuSE Linux Enterprise Server (SLES), and OpenSuSE). 

DistroWatch.com is a website to stay on top of new distributions available. 

The most common distros used in professional development are RHEL and Ubuntu. 
- RHEL is used most commonly at bank, airline, telecom, and healthcare organizations. To run RHEL, the license must be paid for. However, CentOS is an RHEL derivative that is free to use. 
- Ubuntu is most commonly used at startups, for SaaS (Software as a Service), social networks, and companies that rely on cloud-based platforms. 

Other non-business distros are Linux Mint, Debian, Mageia, Fedora, openSUSE, Arch Linux, and Slackware. 

Ultimately, Linux is Linux at the core, and choosing a distro over another doesn't have the potential to be the 'wrong' choice, per se. 

## Install Linux

Installation procedures vary between Windows and Mac. For all procedures, virtualization software is needed to install a virtual machine on top of an existing operating system. For Windows, [VirtualBox](https://www.virtualbox.org/) is an example of virtualization software to install a full Linux distro as a virtual machine (VM) on top of Windows. 

Common issues that may arise for booting a VM on Windows may be related to present anti-virus software. Disable the anti-virus software and/or restart the computer, then restart the VM. 

## Getting Connected: Log into Linux, SSH

If an OS image was used to install the distro as a VM, ensure the login information is known to access the desktop. 

If Linux is installed on a local machine, it's possible to access it through its GUI and terminal through virtualization software, like VirtualBox. However, if the connection needs to be established over the internet to a remote Linux server, an SSH or Telnet connection will need to be made to it. 

SSH (Secure Shell) is a network protocol whose primary purpose is to connect from one system to another over a network. SSH has replaced Telnet, a practically obsolete and less secure system. However, it may be needed for legacy systems. 

In order to connect to Linux over the network, a terminal emulator will be needed. For Windows and Unix, [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/) is a free implementation of SSH and Telnet. 

## Common Directories
The most commonly accessed top-level directories include: 
- `/` - "root", the top of the file system hierarchy. 
- `/bin` - binaries and other executable programs. Some applications may be located here. 
- `/etc` - system configuration files. Control how applications and systems behave. 
- `/home` - home directories stated here. Stores separation of data between users. 
- `/opt` - optional or third party software that didn't come with the OS. 
- `/tmp` - for temporary space, typically cleared on reboot. Long-term data/files should not be stored here. 
- `/usr` - user related programs. Subdirectories like `bin/` within user contain binaries/executables for these programs, and `local/` for third-party apps. 
- `/var` - variable data, most notably log files (generated by OS or applications). 

Other directories include: 
- `/export` - shared file systems
- `/lib` - system libraries
- `/lib64` - system libraries in 64-bit
- `/lost+found` - used by file system (fs) to store recovered files after a file system check has been performed
- `/media` - used to mount removable media like CD-ROMs. `/cdrom` is an alternative naming for this purpose on other distros. 
- `/mnt` - used to mount external file systems
- `/proc` - provides info about running processes
- `/root` - home directory for root account
- `/sbin` - system administration binaries
- `/srv` - used by OS to place data that is served by the Linux server (ex. web files, FTP)

Applications that are installed to a Linux OS that weren't bundled with it may be installed in `/usr/local/...`, with the application name replacing the dots. Subdirectories for that application are placed in the application's folder. For example, for an application named `hello`, `/usr/local/hello/bin` would contain binary/executable programs for the Hello application, `/usr/local/hello/etc` would contain system config files for Hello, and so on. 

Application installations won't always follow this strict pattern. The following directory structure can be seen as well, for one application installation: 

```
/etc/opt/hello
/opt/hello/bin
/opt/hello/lib
/var/opt/myapp
```

## Linux Shell
The shell, AKA command line interpreter (CLI), is an application or program that accepts and executes commands given to it. The shell is the default interface to Linux, especially when connecting to a remote Linux server via an SSH (Secure SHell). Server distros do not include GUIs, and thus interacting with it via shell is required. Desktop distros have both GUIs and CLIs. If interacting first through GUI, find the terminal emulator to gain access to the shell if needed. 

### The Prompt

If logged in as a user, will see `[username@name-of-linux-system-connected] ~]$` (ends in `$`). Day-to-day activities are done and user-level applications are controlled using normal accounts like this. 

If logged in as a superuser, will see `[root@name-of-linux-system:~]#` (ends in `#`). The superuser is AKA the root account. Root access is typically restricted to system admins. Access may be required to install, start, or stop system-level applications. 

Shorthands abstract away some of the complexity in prompts. 
- The tilde `~` represents a home directory. Used by itself, it represents the current user's home or account directory. But occasionally, accounts can be represented by other entities, like servers. 
  - `~vik` = /home/vik
  - `~bob` = /home/bob
  - `~root` = /root
  - `~ftp` = /srv/ftp (server account lives in /srv)

Shell prompts can vary greatly in appearance. 

## Basic Linux Commands
- `ls`: lists directory contents
  - `-l`: long listing format: appends more detailed information on the content
- `cd`: changes current directory. Without an argument after, goes back to home directory. 
- `pwd`: displays present working directory
- `cat`: concatenates and displays files of the file provided as an argument
  - `tac`: displays files in reverse order
- `echo`: displays arguments to the screen; displays contents of variables, such as environment variables
  - Environment variables are storage locations that contain name-value pairs. All the letters in the variable are upper-cased (i.e. `$VAR_NAME`). 
  - PATH is an environment variable that controls the command search path and contains a list of directories that are separated by a `:`. If a command is entered into the prompt, the command is searched for in the PATH. If PATH = `/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/sbin:/home/jason/bin`, every directory will be searched for the command. 
    - If it's found in one, it will execute there. 
    - If it isn't found, the prompt will display `command not found`. 
    - If it's found in multiple directories (i.e. `/bin/cat` and `/usr/local/bin`), the command will execute in the directory it's found in first in PATH. 
- `man`: displays the online manual. If command name given as argument, displays manual for that command
  - `-k`: search man pages
  - Using 'Enter' key goes down the file by 1 line. 
  - Using 'Space' goes down the file by 1 page. 
  - Using 'g' goes to the very top of the page. 
  - Using 'G' goes to the very bottom. 
  - Using 'q' quits out of the file. 
- `exit`: exits the shell or current session. 
- `clear`: clears the screen. 
- `which`: locate a command (i.e. `which cat` -> `/bin/cat`).
  - The location of a command can be used in place of the command itself (i.e. `cat sales.data` will show the file sales.data, as does `/bin/cat sales.data`). 
- `--help`, `-h`: ask commands for help. 

## Working With Directories
Directories are containers for files and other directories. They provide a tree-like structure and can be accessed by name or shortcut. 

- `.`: this directory. 
- `..`: parent directory. 
- `cd -`: change to previous directory. 
  - `echo $OLDPWD`: `$OLDPWD` variable holds the directory previously in, thus performing `echo` on this lists that directory. 
- `/`: directory separator; denotes the ending of a directory. 
- `./<program>`: executes a program from the current directory. 
- `mkdir [-p] <name>`: create a directory. 
  - `[-p]` is an optional argument that creates each directory listed as a new parent (i.e. `mkdir -p one/two/three` creates `one` as a new directory, `two` directory as a child of `one`, and `three` as a child of two). 
- `rmdir [-p] <name>`: remove directory (empty only). 
- `rm -rf <name>`: recursively removes directory and everything below it. 

## Listing Files and Understanding LS Output
- `ls`: lists basic information about a directory's content and information. Doesn't specify file type. 
- `ls -l`: lists detailed information about a current directory's content and info. 
  - Example: `ls -l` -> `-rw-rw-r-- 1 vik users 10400 Sep 27 08:52 sales.data`
    - From left to right: permissions, number of links, owner name, group name, number of bytes in the file, last modified (date and time), file name
- `ls -a`: lists basic information, inclusive of hidden files/folders. 
- `ls -l -a`: lists detailed information of both visible and hidden files/folders. 
  - Shorthand is `ls -la`. 
- `ls -F`: lists directory content along with file types. 
  - `-F` appends specifying character to directory/file name to reveal its file type. Characters:
    - `/`: directory
    - `@`: link
    - `*`: executable
- `ls -t`: lists files by time. 
- `ls -r`: reverse order. 
- `ls -latr`: long listing including all files reverse-sorted by time. Especially useful if need to list an overflowing number of files in a directory, but sorted from least to most recently modified. `ls -lat` shows most to least recently modified order. 
- `ls -R`: lists files recursively; lists current directory's files and directories' files below, recursively. 
- `tree`: lists files recursively in visual format. 
  - `tree -d`: lists directories only. 
  - `tree -C`: colorizes visual output. 
- `ls --color`: basic list output colorized by file type. 
- To circumvent issues with file names with spaces, encapsulate file name in single or double quotes (i.e. `ls -l 'my notes.txt'`, `ls -l "my notes.txt'`) or escape the space with a backslash `\` (i.e. `ls -l my\ notes.txt`). 

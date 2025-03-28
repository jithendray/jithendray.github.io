---
layout: post
title: Linux Commands
tags:
  - linux
---
### **File and Directory Management**  
- `ls` – List directory contents  
- `pwd` – Print current working directory  
- `cd [directory]` – Change directory  
- `mkdir [dir]` – Create a new directory  
- `rmdir [dir]` – Remove an empty directory  
- `rm -r [dir/file]` – Remove directory or file recursively  
- `cp [source] [destination]` – Copy files or directories  
- `mv [source] [destination]` – Move/rename files  
- `find [path] -name [filename]` – Search for files by name  

---

### **File Operations**  
- `cat [file]` – Display file contents  
- `tac [file]` – Display file contents in reverse  
- `less [file]` – View file content page by page  
- `more [file]` – Similar to `less`, but less advanced  
- `head -n [num] [file]` – Show first `n` lines of a file  
- `tail -n [num] [file]` – Show last `n` lines of a file  
- `touch [file]` – Create an empty file or update timestamp  
- `stat [file]` – Display file metadata  
- `diff [file1] [file2]` – Compare two files  

---

### **Permissions and Ownership**  
- `ls -l` – Show file permissions and ownership  
- `chmod [mode] [file]` – Change file permissions (`chmod 755 file`)  
- `chown [user]:[group] [file]` – Change file owner  
- `chgrp [group] [file]` – Change file group  

---

### **Process Management**  
- `ps aux` – Show running processes  
- `top` – Display real-time process usage  
- `htop` – Interactive process viewer (if installed)  
- `kill [PID]` – Terminate process by PID  
- `killall [name]` – Kill all processes by name  
- `pkill [pattern]` – Kill processes matching a pattern  
- `jobs` – Show background jobs  
- `fg` – Bring background job to foreground  
- `bg` – Resume a background job  
- `nohup [command] &` – Run a process in the background  

---

### **Networking**  
- `ip a` – Show IP address configuration  
- `ifconfig` – Deprecated alternative to `ip a`  
- `ping [host]` – Test network connection  
- `curl [url]` – Fetch data from a URL  
- `wget [url]` – Download files  
- `netstat -tulnp` – Show open ports and services  
- `ss -tulnp` – Modern alternative to `netstat`  
- `traceroute [host]` – Trace network path to a host  
- `nslookup [domain]` – Query DNS records  

---

### **User Management**  
- `whoami` – Show current user  
- `who` – Show logged-in users  
- `id [user]` – Show user’s UID and GID  
- `su [user]` – Switch to another user  
- `sudo [command]` – Run command as superuser  
- `passwd [user]` – Change user password  
- `useradd [user]` – Create a new user  
- `usermod -aG [group] [user]` – Add user to a group  
- `userdel [user]` – Delete a user  

---

### **Disk and Storage**  
- `df -h` – Show disk space usage  
- `du -sh [dir]` – Show size of a directory  
- `mount [device] [mountpoint]` – Mount a filesystem  
- `umount [device]` – Unmount a filesystem  
- `lsblk` – List all block devices  
- `fdisk -l` – Show disk partitions  
- `mkfs.ext4 /dev/[device]` – Format a disk partition  

---

### **Package Management**  

#### **Debian/Ubuntu (APT)**
- `apt update` – Update package lists  
- `apt upgrade` – Upgrade all installed packages  
- `apt install [package]` – Install a package  
- `apt remove [package]` – Remove a package  

#### **Arch Linux (Pacman)**
- `pacman -Syu` – Sync and update system  
- `pacman -S [package]` – Install package  
- `pacman -R [package]` – Remove package  

#### **Red Hat/CentOS (Yum/DNF)**
- `yum update` or `dnf update` – Update packages  
- `yum install [package]` – Install package  
- `yum remove [package]` – Remove package  

---

### **System Monitoring**  
- `uptime` – Show system uptime  
- `free -h` – Show memory usage  
- `vmstat` – Show system performance metrics  
- `iostat` – Show CPU and disk I/O stats  
- `dmesg | tail` – Show kernel logs  
- `journalctl -xe` – Show detailed system logs  
- `history` – Show command history  

---

### **Archiving and Compression**  
- `tar -cvf archive.tar [file/dir]` – Create tar archive  
- `tar -xvf archive.tar` – Extract tar archive  
- `tar -czvf archive.tar.gz [file/dir]` – Create tar.gz archive  
- `tar -xzvf archive.tar.gz` – Extract tar.gz archive  
- `zip [file.zip] [file]` – Create ZIP archive  
- `unzip [file.zip]` – Extract ZIP archive  

---

### **Text Processing**  
- `grep [pattern] [file]` – Search text in a file  
- `awk '{print $1}' file` – Process text by columns  
- `sed 's/old/new/g' file` – Replace text in a file  
- `cut -d':' -f1 /etc/passwd` – Extract fields from text  
- `sort [file]` – Sort file content  
- `uniq [file]` – Remove duplicate lines  

---

### **Shell Scripting and Automation**  
- `echo "Hello"` – Print text  
- `read var` – Take user input  
- `export VAR=value` – Set environment variable  
- `crontab -e` – Edit cron jobs  
- `chmod +x script.sh` – Make script executable  
- `./script.sh` – Run a script  

---

### **Miscellaneous**  
- `alias ll='ls -lah'` – Create alias  
- `unalias ll` – Remove alias  
- `time [command]` – Measure execution time  
- `watch -n 5 [command]` – Run command every 5 seconds  
- `yes | command` – Auto-confirm prompts  
- `sleep 5` – Wait for 5 seconds  
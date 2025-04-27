# Linux & DevOps Interview Prep

This repository contains a collection of commonly asked Linux and DevOps-related interview questions and answers, designed to help you prepare for roles such as Site Reliability Engineer (SRE) or DevOps Consultant.

## Questions & Answers

### 1. How to find a process running on port 8080 in Linux?

To find a process running on port 8080, you can use the following commands:
```bash
sudo lsof -i :8080
```
Or:
```bash
netstat -tuln | grep 8080
```
These commands will list the process that is using port 8080.

### 2. How to troubleshoot disk full issue on a Linux server?

To troubleshoot a disk full issue:
1. Use `df -h` to check disk space usage across partitions.
2. Use `lsblk` to list block devices.
3. Clean up unnecessary files and logs in case of disk space overload.
4. If needed, add a new disk, format it, mount it, and update `/etc/fstab` for persistent mounting.

### 3. How comfortable are you working on Linux servers?

Basic commands for Linux servers:
- **Process Management**: `ps`, `top`, `kill`, `htop`
- **Disk Usage**: `df -h`, `du -sh`
- **Network Troubleshooting**: `ping`, `netstat`, `ss`, `traceroute`, `curl`
- **File Permissions**: `chmod`, `chown`, `chgrp`

### 4. How would you give read/write access to a user on a specific directory?

You can give read/write access to a user by using the `chmod` and `chown` commands. For example:
```bash
sudo chown user:user /path/to/directory
sudo chmod 755 /path/to/directory
```
This sets the owner to `user`, grants read/write/execute permissions to the owner, and read/execute permissions to others.

### 5. How to check if a port is open/listening on a Linux machine?

To check if a port is open or listening, use the following commands:
```bash
sudo netstat -tuln | grep :<port>
```
Or use `ss`:
```bash
sudo ss -tuln | grep :<port>
```
These commands will show you which services are listening on the specified port.

### 6. What's the difference between a hard link and a soft link?

- **Hard Link**: A hard link creates an additional directory entry for a file, pointing to the same inode. Both links are indistinguishable, and the file is deleted only when all hard links are removed.
- **Soft Link (Symbolic Link)**: A soft link points to a file or directory by its path. If the target file is moved or deleted, the soft link will be broken.

### 7. How would you schedule a cron job to run every 15 minutes?

You can schedule a cron job to run every 15 minutes by adding the following entry in the crontab:
```bash
*/15 * * * * <command>
```
This will run `<command>` every 15 minutes.

---

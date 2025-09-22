# Red Hat Certified System Administrator (RHCSA)

1) Red Hat System Adminitrator I (RH124)
2) Red Hat System Adminitrator II (RH134)

---
# RHCSA Exam Objectives

As with all Red Hat performance-based exams, configurations must persist after reboot without intervention.

---

## 1. Understand and use essential tools
- Access a shell prompt and issue commands with correct syntax  
- Use input-output redirection (`>`, `>>`, `|`, `2>`, etc.)  
- Use `grep` and regular expressions to analyze text  
- Access remote systems using SSH  
- Log in and switch users in multiuser targets  
- Archive, compress, unpack, and uncompress files using `tar`, `gzip`, and `bzip2`  
- Create and edit text files  
- Create, delete, copy, and move files and directories  
- Create hard and soft links  
- List, set, and change standard `ugo/rwx` permissions  
- Locate, read, and use system documentation (`man`, `info`, `/usr/share/doc`)  

---

## 2. Manage software
- Configure access to RPM repositories  
- Install and remove RPM software packages  
- Configure access to Flatpak repositories  
- Install and remove Flatpak software packages  

---

## 3. Create simple shell scripts
- Conditionally execute code (`if`, `test`, `[ ]`)  
- Use looping constructs (`for`, etc.) to process files or input  
- Process script inputs (`$1`, `$2`, etc.)  
- Process output of shell commands within a script  

---

## 4. Operate running systems
- Boot, reboot, and shut down a system normally  
- Boot systems into different targets manually  
- Interrupt the boot process in order to gain access  
- Identify CPU/memory intensive processes and kill processes  
- Adjust process scheduling (`nice`, `renice`)  
- Manage tuning profiles  
- Locate and interpret system log files and journals  
- Preserve system journals  
- Start, stop, and check the status of network services  
- Securely transfer files between systems  

---

## 5. Configure local storage
- List, create, delete partitions on MBR and GPT disks  
- Create and remove physical volumes  
- Assign physical volumes to volume groups  
- Create and delete logical volumes  
- Configure systems to mount file systems at boot by UUID or label  
- Add new partitions, logical volumes, and swap to a system non-destructively  

---

## 6. Create and configure file systems
- Create, mount, unmount, and use VFAT, ext4, and XFS file systems  
- Mount and unmount NFS network file systems  
- Configure `autofs`  
- Extend existing logical volumes  
- Diagnose and correct file permission problems  

---

## 7. Deploy, configure, and maintain systems
- Schedule tasks using `at` and `cron`  
- Start and stop services, configure them to start at boot  
- Configure systems to boot into a specific target automatically  
- Configure time service clients (`chrony`, `timedatectl`)  
- Install and update software packages from CDN, repository, or local file system  
- Modify the system bootloader  

---

## 8. Manage basic networking
- Configure IPv4 and IPv6 addresses  
- Configure hostname resolution  
- Configure network services to start automatically at boot  
- Restrict network access using `firewalld` and `firewall-cmd`  

---

## 9. Manage users and groups
- Create, delete, and modify local user accounts  
- Change passwords and configure password aging (`chage`)  
- Create, delete, and modify groups and memberships  
- Configure superuser access (`sudo`)  

---

## 10. Manage security
- Configure firewall settings using `firewall-cmd` / `firewalld`  
- Manage default file permissions (`umask`)  
- Configure key-based SSH authentication  
- Set enforcing and permissive modes for SELinux  
- List and identify SELinux file and process context  
- Restore default file contexts (`restorecon`)  
- Manage SELinux port labels  
- Use boolean settings to modify SELinux configuration  

---

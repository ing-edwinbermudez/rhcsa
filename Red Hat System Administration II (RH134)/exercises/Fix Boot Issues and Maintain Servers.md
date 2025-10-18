# Lab: Fix Boot Issues and Maintain Servers

## Specifications

You are a Linux system administrator at Quasar Technologies, an IT services company that provides managed hosting and cloud infrastructure to clients. Your duties include maintaining server stability, troubleshooting issues, and implementing automation to support the operations of clients.

- On the workstation machine, run the `/tmp/rhcsa-break1` script. This script creates an issue with the boot process on the serverb machine and then reboots the serverb machine.

```bash
bash /tmp/rhcsa-break1
```



- A client opened a case reporting that the `serverb` machine is down after rebooting the machine during maintenance tasks. The case description mentions that the server is stuck at boot with errors related to mounting a partition. You have been asked to investigate and to fix the issue.

    - Access the console for the serverb machine and boot into emergency mode for maintenance. Look for any error messages on the console that relate to a problem with mounting a partition. Use redhat as the password.

    - Remount the root file system in read/write mode.

    - Try to mount all the other file systems and identify the file system that fails to mount.

    - Edit the /etc/fstab file to fix the issue. Remove or comment out the incorrect line.

    - Reboot the serverb machine and confirm that the system now boots without errors.


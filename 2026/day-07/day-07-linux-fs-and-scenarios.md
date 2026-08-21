Day 07 – Linux File System & Scenario-Based Practice

Directory	Purpose	I would use this when...
/	Starting point of the Linux file system.	I need to understand the system structure.
/home	Contains normal users' home directories.	I need to access user files.
/root	Home directory of the root user.	I need to access root user files.
/etc	Contains system configuration files.	I need to check system settings.
/var/log	Stores system and application logs.	I need to troubleshoot errors.
/tmp	Stores temporary files.	I need temporary storage.
/bin	Contains essential Linux commands.	I need basic system commands.
/usr/bin	Contains user programs and commands.	I need to locate installed commands.
/opt	Used for optional or third-party software.	I need to find additional applications.
Useful Commands
# Find large log files
du -sh /var/log/* 2>/dev/null | sort -h | tail -5

# Check hostname
cat /etc/hostname

# Check home directory
ls -la ~

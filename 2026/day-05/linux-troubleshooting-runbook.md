# Day 05 – Linux Health Check & Troubleshooting Runbook

## Objective

Perform a basic Linux health check, inspect a running service, review system logs, and document a repeatable troubleshooting process.

The main goal is to **collect evidence before taking corrective action**.

---

# 1. Environment Verification

Before troubleshooting, first understand which Linux system and kernel I am working on.

## Check Kernel and System Information

```bash
uname -a
```

### Purpose

`uname` displays information about the Linux kernel and system.

`-a` means **all available information**.

### Important Information

* Hostname
* Kernel version
* CPU architecture
* Operating system/kernel information


### Observation

The command confirms the Linux kernel version, hostname, and system architecture.

---

## Check Linux Distribution

```bash
lsb_release -a
```

If `lsb_release` is unavailable:

```bash
cat /etc/os-release
```

### Purpose

This identifies the Linux distribution and version.

For example:

```text
Ubuntu
Debian
RHEL
CentOS
Amazon Linux
```

This is important because package-management and administration commands can differ between distributions.

### My Output

```text
PASTE YOUR ACTUAL OUTPUT HERE
```

### Observation

The command confirms the Linux distribution and release version.

---

# 2. Filesystem Sanity Check

Before troubleshooting applications, verify that the filesystem is working and writable.

## Create a Temporary Directory

```bash
mkdir /tmp/runbook-demo
```

### Purpose

`mkdir` means **make directory**.

The command creates a temporary directory that can be used for testing.

### Observation

The directory was created successfully, confirming that I have permission to create files in `/tmp`.

---

## Copy a File

```bash
cp /etc/hosts /tmp/runbook-demo/hosts-copy
```

### Purpose

`cp` copies a file from one location to another.

This verifies that the system can:

* Read the source file
* Write to the destination
* Create a new file

### Observation

The `/etc/hosts` file was copied successfully.

---

## Check the File

```bash
ls -l /tmp/runbook-demo
```

### Purpose

`ls` lists files.

`-l` provides a detailed/long listing including:

* Permissions
* Owner
* Group
* File size
* Modification time
* Filename

### Observation

The copied file exists and its permissions, owner, and size can be verified.

---

# 3. CPU & Memory Health

## Check Running Processes

```bash
top
```

### Purpose

`top` provides a live view of running processes and system resource usage.

It helps identify:

* High CPU usage
* High memory usage
* Resource-intensive processes
* System load

### Important Fields

```text
PID
%CPU
%MEM
COMMAND
```

`PID` = Process ID

`%CPU` = CPU consumed by the process

`%MEM` = Memory consumed by the process

`COMMAND` = Process/program name

Press `q` to exit `top`.

### Observation

Check whether any process is consuming unusually high CPU or memory.

---

## Check a Specific Process

First find the process ID:

```bash
pgrep sshd
```

Then:

```bash
ps -o pid,pcpu,pmem,comm -p <PID>
```

### Purpose

`ps` provides a snapshot of process information.

Unlike `top`, which continuously updates, `ps` gives a point-in-time view.

### Options

```text
-o      Select the output columns
pid     Process ID
pcpu    CPU percentage
pmem    Memory percentage
comm    Command/process name
-p      Select a specific PID
```

### Observation

The command shows the CPU and memory consumption of the selected service/process.

---

## Check Memory

```bash
free -h
```

### Purpose

Displays RAM and swap memory information.

`-h` means **human-readable**.

Instead of:

```text
7856232
```

it displays values such as:

```text
7.5Gi
```

### Important Fields

```text
total
used
free
buff/cache
available
```

The `available` value is especially useful when determining whether the system has enough memory for new applications.

### Observation

Check whether available memory is healthy or whether the system is under memory pressure.

---

# 4. Disk & I/O Health

## Check Filesystem Usage

```bash
df -h
```

### Purpose

`df` means **disk filesystem**.

It shows how much space is:

* Used
* Available
* Allocated

`-h` makes the output human-readable.

### Important Field

```text
Use%
```

Example:

```text
45%
```

means approximately 45% of that filesystem is being used.

### Why It Matters

A filesystem approaching 100% can cause:

* Applications to fail
* Logs to stop writing
* Databases to experience problems
* Temporary files to fail
* Services to malfunction

### Observation

Check whether any filesystem has critically high usage.

---

## Check Log Directory Size

```bash
du -sh /var/log
```

### Purpose

`du` means **disk usage**.

Unlike `df`, which shows filesystem-level usage, `du` helps determine how much space a particular directory consumes.

Options:

```text
-s = summary
-h = human-readable
```

### Observation

Check whether `/var/log` is consuming an unusually large amount of disk space.

---

## Check System I/O and Memory Activity

```bash
vmstat
```

### Purpose

`vmstat` provides information about system activity such as:

* Processes
* Memory
* Swap
* CPU
* I/O

It can help identify whether the system is experiencing CPU or I/O pressure.

### Observation

Check for unusual CPU wait, swapping, or I/O activity.

---

# 5. Network Health

## Check Listening Ports

```bash
ss -tulpn
```

### Purpose

`ss` displays socket/network information.

It helps determine which services are listening for network connections.

### Options

```text
-t = TCP
-u = UDP
-l = Listening
-p = Process information
-n = Numeric addresses/ports
```

For example:

```text
*:22
```

usually indicates a service listening on SSH port 22.

### Observation

Verify that the expected service is listening on its required port.

---

## Test HTTP Service

```bash
curl -I http://localhost
```

### Purpose

`curl` is a command-line tool for communicating with servers.

`-I` requests only the HTTP headers.

Example:

```text
HTTP/1.1 200 OK
```

A `200 OK` response indicates that the HTTP service responded successfully.

Other responses may indicate different conditions:

```text
200 = Successful
404 = Resource not found
500 = Server-side error
Connection refused = Nothing accepting the connection on that port
```

### Observation

Record the actual HTTP response from the local service.

---

# 6. Service Inspection

Choose one service and use it consistently during the troubleshooting drill.

Example:

```text
sshd
```

or:

```text
ssh
```

depending on the Linux distribution.

---

## Check Service Status

```bash
systemctl status <service-name>
```

Example:

```bash
systemctl status ssh
```

or:

```bash
systemctl status sshd
```

### Purpose

`systemctl` is used to manage and inspect services controlled by `systemd`.

`status` shows information such as:

* Whether the service is running
* Whether it failed
* Process ID
* Recent service messages
* When it started

### Common States

```text
active (running)
inactive
failed
```

### Observation

Record whether the selected service is currently running successfully.

---

# 7. Service Logs

## Review Recent Service Logs

```bash
journalctl -u <service-name> -n 50
```

Example:

```bash
journalctl -u ssh -n 50
```

### Purpose

`journalctl` reads logs collected by the `systemd` journal.

Options:

```text
-u ssh = Show logs for the SSH service
-n 50  = Show the latest 50 lines
```

### What to Look For

* Errors
* Warnings
* Service crashes
* Authentication failures
* Startup failures
* Repeated messages

### Observation

Record whether recent logs contain errors or warnings.

---

# 8. Read Traditional Log Files

```bash
tail -n 50 /var/log/<log-file>.log
```

Example:

```bash
tail -n 50 /var/log/auth.log
```

### Purpose

`tail` displays the end of a file.

`-n 50` means show the last 50 lines.

This is useful because recent log entries are usually the most relevant during an incident.

### Follow Logs in Real Time

```bash
tail -f /var/log/auth.log
```

`-f` means **follow**.

It keeps the command running and displays new log entries as they are written.

Press:

```text
Ctrl + C
```

to stop following the log.

---

# 9. Writing and Reading Files

During Linux troubleshooting, it is also important to understand basic file manipulation.

## Create/Overwrite a File

```bash
echo "Line 1" > notes.txt
```

`echo` prints text.

`>` redirects the output into a file.

Important:

```text
> = overwrite
```

If `notes.txt` already contains information, `>` replaces its contents.

---

## Append to a File

```bash
echo "Line 2" >> notes.txt
```

`>>` adds the text to the end of the existing file.

Remember:

```text
>  = overwrite
>> = append
```

After running:

```bash
echo "Line 1" > notes.txt
echo "Line 2" >> notes.txt
```

the file contains:

```text
Line 1
Line 2
```

---

## Using `tee`

```bash
echo "Line 3" | tee -a notes.txt
```

### Purpose

The pipe:

```text
|
```

takes the output of one command and sends it as input to another command.

`tee` sends the input to both:

1. The terminal
2. A file

`-a` means append.

Therefore:

```bash
echo "Line 3" | tee -a notes.txt
```

will display:

```text
Line 3
```

on the terminal and also append it to `notes.txt`.

The final file becomes:

```text
Line 1
Line 2
Line 3
```

---

# 10. Reading Files

## Read a Small File

```bash
cat notes.txt
```

`cat` displays the contents of a file.

---

## Read Large Files

```bash
less notes.txt
```

`less` allows the file to be viewed page by page.

Press:

```text
q
```

to quit.

---

## First Lines

```bash
head notes.txt
```

Displays the first 10 lines by default.

---

## Last Lines

```bash
tail notes.txt
```

Displays the last 10 lines by default.

---

# Mini Runbook

## Troubleshooting Sequence

When a Linux service has a problem, I will follow this general sequence:

```text
1. Identify the system
        ↓
2. Check filesystem
        ↓
3. Check CPU
        ↓
4. Check memory
        ↓
5. Check disk
        ↓
6. Check I/O
        ↓
7. Check network
        ↓
8. Check service status
        ↓
9. Check service logs
        ↓
10. Decide next action
```

---

# Quick Findings

Record your actual observations here.

### CPU

```text
Example:
CPU usage was normal and no process showed abnormal CPU consumption.
```

### Memory

```text
Example:
Available memory was healthy and no obvious memory pressure was observed.
```

### Disk

```text
Example:
Filesystem usage was below the critical threshold and sufficient free space remained.
```

### Network

```text
Example:
The expected service port was listening and the local HTTP endpoint responded successfully.
```

### Service

```text
Example:
The selected service was active and running.
```

### Logs

```text
Example:
The latest 50 log entries contained no critical errors or repeated failures.
```

---

# If the Situation Were Worse

If the service or system becomes unhealthy, I would:

1. **Collect evidence first** — capture CPU, memory, disk, network, service status, and logs before making changes.

2. **Investigate the specific problem** — identify high CPU processes, memory pressure, full filesystems, network issues, or repeated application errors.

3. **Take corrective action** — restart the affected service if appropriate, free disk space, stop/optimize problematic processes, or correct configuration.

4. **Monitor after the change** — verify service status and watch logs using `journalctl` or `tail -f`.

5. **Escalate if required** — provide the timestamps, commands, outputs, logs, and actions already performed.

---

# Key Commands Learned

| Area        | Command               | Main Purpose                     |
| ----------- | --------------------- | -------------------------------- |
| System      | `uname -a`            | Kernel/system information        |
| OS          | `cat /etc/os-release` | Linux distribution               |
| Files       | `mkdir`               | Create directory                 |
| Files       | `cp`                  | Copy files                       |
| Files       | `ls -l`               | Detailed file information        |
| CPU         | `top`                 | Live process/resource monitoring |
| CPU         | `ps`                  | Process snapshot                 |
| Memory      | `free -h`             | RAM/swap information             |
| Disk        | `df -h`               | Filesystem capacity              |
| Disk        | `du -sh`              | Directory size                   |
| I/O         | `vmstat`              | CPU/memory/I/O statistics        |
| Network     | `ss -tulpn`           | Listening ports/connections      |
| HTTP        | `curl -I`             | Test HTTP response               |
| Services    | `systemctl status`    | Service status                   |
| Logs        | `journalctl`          | systemd service logs             |
| Logs        | `tail`                | Read recent log entries          |
| Files       | `echo`                | Print/write text                 |
| Redirection | `>`                   | Overwrite file                   |
| Redirection | `>>`                  | Append to file                   |
| Pipeline    | `\|`                  | Send output to another command   |
| Files       | `tee -a`              | Display and append output        |

---

# Final Outcome

This exercise builds a repeatable troubleshooting habit:

**Observe → Collect evidence → Identify the problem → Take action → Verify → Escalate if necessary**

The most important lesson is:

> **Do not restart a service blindly. Collect evidence first.**

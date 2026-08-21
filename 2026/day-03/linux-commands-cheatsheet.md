# Day 03 – Linux Commands Cheat Sheet

> **#90DaysOfDevOps Challenge – Day 03**

## 🎯 Objective

Practice commonly used Linux commands for:

* File and directory management
* Process monitoring
* Disk and memory checking
* Basic network troubleshooting

---

# ⚙️ Process Management

These commands help us **view and manage running processes**.

| Command        | Use                            |
| -------------- | ------------------------------ |
| `ps aux`       | Show all running processes     |
| `top`          | Monitor processes in real time |
| `pgrep <name>` | Find a process PID             |
| `pstree`       | Show processes in a tree       |
| `kill <PID>`   | Stop a process                 |
| `pkill <name>` | Stop a process by name         |
| `htop`         | Interactive process monitoring |

Example:

```bash
ps aux
```

---

# 📂 File & Directory Commands

These commands are used to **navigate and manage files**.

| Command                   | Use                       |
| ------------------------- | ------------------------- |
| `pwd`                     | Show current directory    |
| `ls -la`                  | List files with details   |
| `cd <directory>`          | Move to another directory |
| `mkdir <directory>`       | Create a directory        |
| `cp source destination`   | Copy a file               |
| `mv source destination`   | Move or rename a file     |
| `rm -rf <directory>`      | Remove a directory        |
| `find /path -name "file"` | Search for a file         |

---

# 💾 Disk Usage Commands

Useful for checking **disk space** on Linux servers.

| Command              | Use                        |
| -------------------- | -------------------------- |
| `df -h`              | Check available disk space |
| `du -sh <directory>` | Check directory size       |

Example:

```bash
df -h
```

This shows how much disk space is **used and available**.

---

# 🌐 Basic Networking Commands

These commands are useful for **network troubleshooting**.

| Command       | Use                        |
| ------------- | -------------------------- |
| `ip addr`     | Show IP addresses          |
| `ping <host>` | Test network connectivity  |
| `curl <URL>`  | Test HTTP/HTTPS connection |

Example:

```bash
ping google.com
```

```bash
curl https://example.com
```

---

# 🧠 Quick Commands to Remember

```text
pwd       → Where am I?
ls        → What is here?
cd        → Move directory
ps        → Show processes
top       → Monitor processes
df -h     → Check disk
free -h   → Check memory
ip addr   → Check IP
ping      → Test connectivity
curl      → Test web connection
```

---

# 📌 Key Takeaways

* Learned basic Linux file and directory commands.
* Practiced checking and managing processes.
* Learned how to check disk and memory usage.
* Practiced basic network troubleshooting.
* These commands are useful for **daily Linux and DevOps troubleshooting**.

### 💡 DevOps Tip

When troubleshooting a Linux server, start with:

```bash
df -h
free -h
ps aux
ip addr
```

These commands quickly tell you about the server's **disk, memory, processes, and network configuration**.

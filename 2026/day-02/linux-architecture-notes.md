# Day 02 – Linux Architecture, Processes & systemd

> **#90DaysOfDevOps Challenge – Day 02**

## 🎯 Objective

Understand the basics of **Linux architecture, processes, and systemd**.

---

## Linux Architecture

```text
Applications
     ↓
User Space
     ↓
Linux Kernel
     ↓
Hardware
```

### Core Components

### 1. Kernel

The **Kernel is the core of Linux**.

It manages:

* CPU
* Memory
* Processes
* Files
* Devices
* Networking

### 2. User Space

This is where normal applications run.

Examples:

* Bash
* Python
* Git
* Docker
* Nginx

Applications communicate with the **Kernel** to use system resources.

### 3. systemd

**systemd** is the main system and service manager in modern Linux.

It is usually **PID 1**.

It is responsible for:

* Starting the system
* Starting services
* Stopping services
* Restarting services
* Managing services

---

## ⚙️ Process Management

A **process is a running program**.

Example:

```bash
python test.py
```

When the program runs, Linux creates a **process**.

Each process has a unique number called **PID (Process ID)**.

### Process Flow

```text
New
 ↓
Running
 ↓
Waiting
 ↓
Terminated
```

### Useful Commands

```bash
ps aux          # Show running processes
top             # Monitor processes
pstree          # Show process tree
kill <PID>      # Stop a process
```

---

## 🔧 Common systemd Commands

Check service:

```bash
systemctl status nginx
```

Start service:

```bash
systemctl start nginx
```

Stop service:

```bash
systemctl stop nginx
```

Restart service:

```bash
systemctl restart nginx
```

Check service logs:

```bash
journalctl -u nginx
```

---

## 📌 5 Commands Used Daily

| Command     | Use               |
| ----------- | ----------------- |
| `ps`        | View processes    |
| `top`       | Monitor processes |
| `systemctl` | Manage services   |
| `df -h`     | Check disk space  |
| `free -h`   | Check memory      |

---

## 📌 Key Takeaways

* **Kernel** → Core of Linux
* **User Space** → Where applications run
* **Process** → Running program
* **PID** → ID of a process
* **systemd** → Manages Linux services
* **PID 1** → Usually systemd
* **systemctl** → Used to manage services

### 💡 DevOps Tip

When a service is not working, first check:

```bash
systemctl status <service>
```

Then check its logs:

```bash
journalctl -u <service>
```

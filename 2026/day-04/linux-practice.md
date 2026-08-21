# Day 04 – Linux Processes, Services & Troubleshooting

> **#90DaysOfDevOps Challenge – Day 04**

## 🎯 Objective

Learn how to check **processes, services, and logs** and understand a simple Linux troubleshooting process.

---

# ⚙️ 1. Checking Processes

A **process** is a program that is currently running.

We can check processes to find out:

* What is running?
* What is the PID?
* Is a particular application running?

### Useful Commands

```bash
ps -ef
```

Shows running processes.

```bash
pgrep nginx
```

Finds the PID of nginx.

---

# 🔧 2. Managing Services

**systemd** manages services in Linux.

For example:

* nginx
* ssh
* docker

### Useful Commands

```bash
systemctl status nginx
```

Check if nginx is running.

```bash
systemctl start nginx
```

Start nginx.

```bash
systemctl stop nginx
```

Stop nginx.

```bash
systemctl restart nginx
```

Restart nginx.

To see running services:

```bash
systemctl list-units --type=service --state=running
```

---

# 📋 3. Checking Logs

Logs help us understand **what went wrong**.

### Using journalctl

```bash
journalctl -u nginx
```

Shows nginx service logs.

To see the latest 20 lines:

```bash
journalctl -u nginx -n 20
```

### Using tail

```bash
tail -n 50 /var/log/nginx/access.log
```

Shows the last 50 lines of the log file.

---

# 🚨 4. Simple Troubleshooting Flow

When a service is not working:

```text
Problem
   ↓
Check Process
   ↓
Check Service Status
   ↓
Check Logs
   ↓
Restart Service
   ↓
Check Again
```

### Example

If nginx is not working:

```bash
ps -ef | grep nginx
```

```bash
systemctl status nginx
```

```bash
journalctl -u nginx -n 20
```

If required:

```bash
systemctl restart nginx
```

Then check again:

```bash
systemctl status nginx
```

---

# 📌 Key Takeaways

* `ps` → Check running processes.
* `pgrep` → Find a process PID.
* `systemctl` → Manage services.
* `journalctl` → Check systemd logs.
* `tail` → View the last lines of a log file.
* Logs are very important for **troubleshooting**.

### 💡 DevOps Tip

Don't immediately restart a service when something fails.

First:

```text
Check → Understand → Fix → Verify
```

This helps you find the **actual cause** of the problem.

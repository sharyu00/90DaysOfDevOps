# 🐧 Day 09 – Linux User & Group Management Challenge

## 📌 Overview
Practiced managing Linux users, groups, and directory permissions using hands-on terminal commands.

---

## 🛠️ User Commands

### 👤 `useradd -m` vs `useradd`
* **`useradd -m <username>`**: Creates a new user **and** automatically builds their home directory (e.g., `/home/username`).
* **`useradd <username>`**: Creates a new user **without** a home directory.
* **`adduser <username>`**: Creates a new user and asks for Password.

**Example:**

sudo useradd -m tokyo
Sudo adduser tokyo

🔍 Command to view users:


cat /etc/passwd
👥 Group Commands
🏷️ groupadd vs gpasswd -a
groupadd <groupname>: Creates a new group on the system.

gpasswd -a <username> <groupname>: Adds an existing user into an existing group.

Example:


# 1. Create a group
sudo groupadd developers

# 2. Add user to the group
sudo gpasswd -a tokyo developers
🔍 Commands to view groups:


# View all system groups
cat /etc/group

# View groups for a specific user
groups tokyo
📁 Shared Directories & Permissions

# Create shared directory with group ownership and 775 permissions
sudo mkdir -p /opt/dev-project
sudo chgrp developers /opt/dev-project
sudo chmod 775 /opt/dev-project
🔍 Command to view directory permissions:


ls -ld /opt/dev-project
🧠 What I Learned
🔐 Created users with home directories using useradd -m.

🏷️ Managed group creations and memberships with groupadd and gpasswd -a.

📂 Secured shared team directories using chgrp and chmod 775.

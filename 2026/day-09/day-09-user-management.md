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

sudo useradd -m tokyo<br>
Sudo adduser tokyo

🔍 Command to view users:<br>
cat /etc/passwd<br>
👥 Group Commands<br>
🏷️ groupadd vs gpasswd -a<br>
groupadd <groupname>: Creates a new group on the system.<br>

gpasswd -a <username> <groupname>: Adds an existing user into an existing group.<br>

Example:<br>


# 1. Create a group
sudo groupadd developers

# 2. Add user to the group
sudo gpasswd -a tokyo developers
🔍 Commands to view groups:


# View all system groups
cat /etc/group

# View groups for a specific user
groups tokyo
📁 Shared Directories & Permissions<br>

# Create shared directory with group ownership and 775 permissions<br>
sudo mkdir -p /opt/dev-project<br>
sudo chgrp developers /opt/dev-project<br>
sudo chmod 775 /opt/dev-project<br>
🔍 Command to view directory permissions:<br>

ls -ld /opt/dev-project


🧠 What I Learned
🔐 Created users with home directories using useradd -m.

🏷️ Managed group creations and memberships with groupadd and gpasswd -a.

📂 Secured shared team directories using chgrp and chmod 775.

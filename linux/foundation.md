# Linux Foundations & Administration

Welcome to the beginning of your Linux journey. This guide covers the core concepts, tools, commands, and operations for using Linux in system admin and security operations.

---

## 1. Introduction to Linux & Architecture

Let's talk basics. Linux is an operating system. Just like Windows and macOS computers run on their respective operating systems, Linux is an operating system for computers too. You may think Linux is niche - not so. Think of any device that does _not_ use Windows or Mac OS, and it probably runs on Linux. This includes Android smartphones, smart TVs, giant internet servers, supercomputers, and more. Linux serves as the baseline operating system for servers, cloud workloads, security tools (such as Kali Linux, Security Onion), and containerized environments.

Why would one use Linux versus other OS? Well, to start off, Linux is open-source, which means that the code it runs on is public. Anyone can look at it, fix bugs on it, and customize it to their own needs and wants. It is completely free to use. Compare this to Windows and Mac OS systems; you cannot look directly at the code easily, it's not free, and one cannot easily modify it. When introducing the basic components of Linux, it can be helpful to compare Linux to something familiar. Let's use a car:

### Core Architecture Components

| Component | Core Role | Car Analogy | What It Actually Does |
| :--- | :--- | :--- | :--- |
| **Kernel** | The **Brain** | The **Engine & Transmission** | • Talks directly to your physical hardware (CPU, RAM).<br>• Controls memory and system security.<br>• Runs silently in the background; you never see it. |
| **Shell** | The **Translator** | The **Steering Wheel & Pedals** | • Acts as the middleman between you and the kernel.<br>• Takes your inputs (typed text commands or mouse clicks).<br>• Translates those inputs into a language the kernel understands. |
| **Distro** | The **Full Package** | The **Finished Vehicle** | • The complete operating system you download and install.<br>• Combines the kernel, shells, and a visual desktop.<br>• Includes pre-installed apps like web browsers and text editors. |


# LINE STOP

| The Kernel | The "brain" that translates commands into physical actions for the hardware on your computer (i.e. telling the screen to display a pixel or the hard drive to save a file) |
| 

+-------------------------------------------------------------------+
|                       The Kernel                         |
|             
          |
+-------------------------------------------------------------------+
|                             Shell                                 |
|                 (Bash, Zsh, Sh - Command Interpreter)             |
+-------------------------------------------------------------------+
|                             Kernel                                |
|     (Process Scheduling, Memory Management, Device Drivers)       |
+-------------------------------------------------------------------+


- **Kernel:** The core interface between system hardware and software processes. Manages memory, CPU allocation, disk I/O, and hardware communication.
- **Shell:** The command-line interface (CLI) interpreter that reads user commands and executes kernel operations (e.g., `bash`, `zsh`).
- **Filesystem Hierarchy Standard (FHS):** Linux organizes all files and devices under a single root directory (`/`).

### Key Directory Structure

| Path | Purpose |
| :--- | :--- |
| `/` | The root directory containing all system files and subdirectories. |
| `/bin` & `/sbin` | Essential user binaries and system administration binaries. |
| `/etc` | System-wide configuration files and service configurations. |
| `/var` | Variable data files, including system logs (`/var/log`) and database storage. |
| `/home` | User home directories containing personal settings and user data. |
| `/proc` & `/sys` | Virtual filesystems exposing kernel variables, device info, and active processes. |
| `/tmp` | Temporary files cleared on reboot or periodically. |

---

## 2. Essential Linux Tools & Utilities

### Package Managers
Package managers handle software installation, dependency resolution, and updates across different distributions.

- **Debian / Ubuntu (`apt`):**
  - Update package lists: `sudo apt update`
  - Upgrade installed software: `sudo apt upgrade -y`
  - Install a tool: `sudo apt install <package_name>`
- **Red Hat / CentOS / Fedora (`dnf` / `yum`):**
  - Install software: `sudo dnf install <package_name>`
  - Search for a package: `dnf search <keyword>`

### Text Editors
System configuration in Linux is file-based. Knowing how to edit files via the terminal is mandatory.

- **Vim / Neovim:** Modal terminal text editor available on virtually all distributions.
  - Insert mode: Press `i`
  - Save and exit: Press `Esc` then type `:wq`
  - Quit without saving: Press `Esc` then type `:q!`
- **Nano:** Beginner-friendly terminal editor with on-screen keyboard shortcuts (`Ctrl+O` to save, `Ctrl+X` to exit).

### Security & Inspection Utilities
- **UFW (Uncomplicated Firewall) / iptables:** Network packet filtering tools.
- **OpenSSH (`ssh`, `sshd`):** Encrypted remote access and file transfer protocols.
- **Sysstat (`sar`, `iostat`):** Performance and resource utilization monitoring tools.

---

## 3. Command Line Reference

### File & Directory Management
```bash
# Display present working directory
pwd

# List directory contents with detailed permissions and hidden files
ls -la

# Change directory
cd /path/to/directory

# Create nested directories
mkdir -p project/logs/2026

# Copy files recursively
cp -r /source/dir /destination/dir

# Move or rename a file
mv old_name.txt new_name.txt

# Remove a file safely / remove directory recursively
rm file.txt
rm -rf directory_name
```

### File Viewing & Manipulation
```bash
# Display full file content
cat /etc/os-release

# Paginate large text files
less /var/log/syslog

# View first 10 or last 20 lines of a file
head -n 10 file.txt
tail -n 20 /var/log/auth.log

# Monitor log entries in real-time
tail -f /var/log/syslog

# Filter text using regular expressions
grep -i "failed" /var/log/auth.log
```

### File Permissions & Ownership
Linux enforces multi-user security through POSIX file permissions (Read, Write, Execute).

```bash
# View permissions
ls -l filename.sh
# Example output: -rwxr-xr-- 1 root admin 1024 Sep 5 12:00 filename.sh

# Modify permissions (Numeric mode: Read=4, Write=2, Execute=1)
chmod 755 filename.sh    # User: rwx (7), Group: r-x (5), Others: r-x (5)
chmod 600 id_rsa         # User: rw- (6), Group: --- (0), Others: --- (0)

# Change file owner and group
sudo chown username:groupname filename.txt
```

### Process Management & System Monitoring
```bash
# View active processes in real time
top
htop    # Interactive alternative (if installed)

# Snapshot active processes filtered by name
ps aux | grep sshd

# Terminate a process by PID or Name
kill -9 <PID>
killall apache2
```

### Networking & Diagnostics
```bash
# Display network interface addresses
ip a

# Check socket statistics and listening ports (replaced netstat)
ss -tulpn

# Test network connectivity and routing
ping -c 4 8.8.8.8
traceroute example.com

# Inspect DNS records
dig example.com
```

### User Administration & Privilege Escalation
```bash
# Execute command with elevated privileges
sudo command

# Switch user to root or target account
sudo -i
su - username

# Create a new user with home directory and bash shell
sudo useradd -m -s /bin/bash newuser

# Change user password
sudo passwd newuser
```

---

## 4. Practical Hands-On Exercises

### Exercise 1: User Audit & Log Searching
1. Search `/var/log/auth.log` (or `/var/log/secure` on RHEL) for failed SSH login attempts:
   ```bash
   grep "Failed password" /var/log/auth.log | awk '{print $11}' | sort | uniq -c
   ```
2. Identify all non-standard users with active shell access in `/etc/passwd`:
   ```bash
   grep -v "nologin\|false" /etc/passwd
   ```

### Exercise 2: File Security Hardening
1. Locate files with SUID permission enabled (potential privilege escalation paths):
   ```bash
   find / -perm -4000 -type f 2>/dev/null
   ```
2. Restrict access to a sensitive configuration file so only the file owner can read and edit it:
   ```bash
   chmod 600 /path/to/sensitive_config.conf
   ```

---

## 5. Next Steps & Learning Resources

- **Interactive Practice:** TryHackMe (Linux Fundamentals modules), OverTheWire (Bandit wargame).
- **Certifications:** CompTIA Linux+, LPI Linux Essentials, Red Hat Certified System Administrator (RHCSA).
- **Official Documentation:** Linux Man Pages (`man command_name`).

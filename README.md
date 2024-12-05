# 🖥️ Born2beroot - System Administration

*This project has been created as part of the 42 curriculum by <ТВОЙ_ЛОГИН>.*

<p align="center">
  <img src="https://img.shields.io/badge/OS-Debian%20%7C%20Rocky-blue" alt="OS">
  <img src="https://img.shields.io/badge/Virtualization-VirtualBox%20%7C%20UTM-orange" alt="Virtualization">
  <img src="https://img.shields.io/badge/School-42-black.svg" alt="School 42">
  <img src="https://img.shields.io/badge/Score-100%2F100-success.svg" alt="Score">
</p>

## 🌟 Description

**Born2beroot** is a System Administration related exercise designed to introduce students to the wonderful world of virtualization. The goal is to create a first machine in VirtualBox (or UTM) using specific, strict instructions to set up a secure, headless operating system.

This project focuses on fundamental sysadmin skills: partition encryption (LVM), security policies (AppArmor/SELinux), firewall configuration (UFW/firewalld), SSH management, strong password policies, and Bash scripting for system monitoring.

## 🏗️ Project Architecture & Design Choices

To comply with the strict rules of the subject, the server was built without any graphical interface (X.org, Wayland) and includes only essential services. 

### ⚙️ OS & Virtualization Choices

| Concept | Comparison & My Choice |
| :--- | :--- |
| **Debian vs Rocky Linux** | **Debian** uses the `apt` package manager and is generally more user-friendly for beginners. It relies on AppArmor for security. **Rocky Linux** is a downstream, complete binary-compatible release using the Red Hat Enterprise Linux (RHEL) source code, utilizing `dnf`/`yum` and SELinux. *I chose [Впиши свой выбор, например: Debian because of its stability and extensive community support for beginners].* |
| **VirtualBox vs UTM** | **VirtualBox** is a powerful x86 and AMD64/Intel64 virtualization product for enterprise as well as home use. **UTM** utilizes Apple's Hypervisor framework and QEMU to emulate different architectures, which is essential for Mac M1/M2 users. *I chose [Впиши свой выбор, например: VirtualBox as I am working on an x86 machine].* |

### 🛡️ Security Implementations

| Technology | Overview |
| :--- | :--- |
| **AppArmor vs SELinux** | Both are Mandatory Access Control (MAC) systems. **AppArmor** (used in Debian) binds access control attributes to programs rather than to users, using file paths. **SELinux** (used in Rocky) is more complex and assigns security contexts to all files, processes, and ports. |
| **UFW vs firewalld** | Both act as front-ends to `iptables`/`nftables`. **UFW** (Uncomplicated Firewall) is standard on Debian and is designed to be easy to use. **firewalld** is the standard for RHEL-based distros (like Rocky) and manages firewall rules dynamically using zones. |

### 📂 Partitioning (LVM)
The system uses Logical Volume Management (LVM) with encrypted partitions. LVM allows for flexible disk management, making it easy to resize volumes dynamically without interrupting the system.

## 📜 Instructions

Since the actual Virtual Machine cannot be uploaded to GitHub (it's strictly forbidden!), this repository only contains:
1. This `README.md` file.
2. `signature.txt` — containing the `sha1` hash of the virtual machine's disk file (`.vdi` or `.qcow2`).

**To verify the machine during evaluation:**
1. Retrieve the signature from the virtual machine file.
   * *Windows:* `certUtil -hashfile <VM_NAME>.vdi sha1`
   * *Linux/macOS:* `shasum <VM_NAME>.vdi`
   * *Mac M1 (UTM):* `shasum <VM_NAME>.utm/Images/disk-0.qcow2`
2. Compare the output with the hash provided in `signature.txt`.

## 📈 Monitoring Script (`monitoring.sh`)

A custom bash script runs every 10 minutes (via `cron`) to broadcast system information to all logged-in users using the `wall` command. It displays:
* Architecture and kernel version
* Physical and virtual CPU count
* Available RAM and disk storage (with utilization percentages)
* CPU load
* Last boot date/time
* LVM status
* Active TCP connections
* Number of users logged in
* Network info (IPv4 and MAC)
* Number of commands executed with `sudo`

## 📚 Resources & AI Usage

* [Debian Official Documentation](https://www.debian.org/doc/)
* [LVM Guide - Arch Wiki](https://wiki.archlinux.org/title/LVM)
* *AI Usage Statement:* AI (ChatGPT/Claude/Gemini) was used strictly as a tutor to explain complex concepts (such as the differences between AppArmor and SELinux, and how cron syntax works). No code or configurations were directly copied, preserving the integrity of the learning process.

---
<p align="center">
  <i>Developed with ☕ and ❤️ at School 42.</i>
</p>

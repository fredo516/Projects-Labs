Completed labs

# 🧪 Linux Server Enumeration & Process Management Lab

## Overview
This lab focused on practicing foundational Linux administration and enumeration techniques commonly used in cybersecurity. The tasks simulate real-world processes such as managing services, monitoring systems, handling automation via cron, and inspecting system logs for activity.

---

## 🔧 Key Concepts Practiced
- Navigated directories using `cd`, `pwd`, and listed contents with `ls`
- Identified running processes using `ps`, `top`, and `htop`
- Found open ports and listening services with `netstat`, `ss`, and `lsof`
- Managed background jobs using `&`, `jobs`, `fg`, and `bg`
- Used `cron` to view and understand scheduled jobs
- Parsed environment variables using the `env` command
- Launched a Python HTTP server to host content using `python3 -m http.server`
- Installed and updated software using `apt-get` and managed repositories with `sources.list`
- Reviewed log files from `/var/log` such as `auth.log`, `syslog`, and `cron.log`

---

## 🛠 Tools Used
- Ubuntu Linux terminal
- Python 3 (for simple HTTP server)
- Core utilities: `ps`, `top`, `kill`, `netstat`, `lsof`, `nano`, `cron`, `cat`, `grep`

---

## 🔐 Real-World Applications
- Process and port enumeration are foundational in threat detection and incident response
- Log file analysis helps track unauthorized access or malware behavior
- Cron job auditing can uncover persistence mechanisms used in attacks
- Running basic HTTP servers is useful for controlled file transfers in red team ops or testing

---

## ✅ Completed By:
**Alfredo San Miguel**  
Documented from TryHackMe/Linux Fundamentals & Enumeration lab work

---
# 🏢 Active Directory Fundamentals Lab

## Overview
This lab explored the basic architecture and practical management of Active Directory environments, including organizing users and systems, creating and delegating permissions, and understanding how domains function within business infrastructures.

---

## 🔧 Key Concepts Practiced
- Understood the function and role of a Domain Controller in centralized Windows administration
- Explored AD structure including Users, Groups, and Organizational Units (OUs)
- Practiced creating, deleting, and managing OUs and security groups
- Assigned and delegated permissions using Active Directory Users and Computers
- Examined the purpose of different built-in security groups (Domain Users, Domain Admins, etc.)

---

## 📊 Tools Used
- Active Directory Users and Computers (Windows Server)
- Domain Services on Windows Server
- Organizational Unit interface, Group Policy delegation panel

---

## 🔐 Real-World Applications
- Administering users and permissions in a centralized enterprise environment
- Recognizing and applying least privilege principles to minimize risk
- Understanding how attackers abuse AD to gain persistence or escalate privileges

---

## ✅ Completed By:
**Alfredo San Miguel**  
Documented from TryHackMe/Windows AD lab work



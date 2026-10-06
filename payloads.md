# Commands Reference
Quick-reference list of commands used in this repo's lab. See README.md for full context, steps, and explanations.

---

## Remote Access

**Connect to the lab server over SSH**
```bash
ssh <username>@<LAB_IP>
```

> The lab password is intentionally not recorded in this repository. Replace `<username>` and `<LAB_IP>` with the values from your own lab dashboard.

---

## System Identity

**Read the OS release file**
```bash
cat /etc/os-release
```

**Show distribution release and description**
```bash
lsb_release -a
```

**Alternatives (not run in this lab, listed for reference)**
```bash
uname -a
hostnamectl
```

---

## Navigation & Filesystem Review

**Show the current working directory**
```bash
pwd
```

**Move into the lab folder**
```bash
cd lab
```

**List contents in long format (type, owner, group, size, date)**
```bash
ls -l
```

**Count the entries that `ls` displays (files and folders together)**
```bash
ls | wc -l
```

**List sorted by size, largest first, with readable sizes**
```bash
ls -lhS
```

**Show hidden files too**
```bash
ls -a
```

**Count only regular files, including inside subfolders**
```bash
find . -type f | wc -l
```

**Look inside the subfolders**
```bash
ls -l backup systembackups
```

**Alternative to list only files in the current folder (not run in this lab)**
```bash
ls -p | grep -v /
```

---

## Access Review (Ownership)

**Check the owner and group of each item**
```bash
ls -l
```

> The third column is the owner and the fourth is the group.

---

## Capacity Baseline

**Check memory (RAM and swap) in readable units**
```bash
free -h
```

**Check disk usage of mounted filesystems**
```bash
df -h
```

**List physical disks and partitions**
```bash
lsblk
```

---

## Process & Service Triage

**Search running processes by name (first attempt)**
```bash
ps aux | grep -i <name>
```

> Problem: `grep` finds its own process, so one line ending in `grep --color=auto -i <name>` does not mean the program is running.

**Check for a real matching process**
```bash
pgrep -l <name>
```

> No output means no matching process is running.

**Fixed version: search several names and hide the grep line**
```bash
ps aux | grep -v grep | grep -iE "<name1>|<name2>|<name3>"
```

> No output means none of those names are running.

**Ask the service manager about a service**
```bash
systemctl status <service>
```

> "Unit ... could not be found" means the service is not installed as a systemd unit, which is stronger evidence than "not running".

**Command that failed the first time**
```text
^[[200~systemctl status <service>
systemctl: command not found
```

> Cause: hidden terminal characters came along with the pasted text. Fix: retype the command by hand.

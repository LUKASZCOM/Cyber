# Windows Cheatsheet

## System Tools (Run with Win+R)
| Command | Description |
|--------|-------------|
| `msconfig` | System configuration (startup, boot, services) |
| `lusrmgr.msc` | Local User and Group Management |
| `compmgmt.msc` | Computer Management (disk, services, users) |
| `msinfo32.exe` | System information (hardware, software, components) |
| `regedit` | Registry editor - configuration database for users/system |
| `resmon` | Resource Monitor (CPU, RAM, disk, network live view) |
| `perfmon` | Performance Monitor (detailed logging over time) |
| `shell:startup` | Autostart apps folder |

## System Variables & Key Paths
- `%windir%` - system variable pointing to Windows directory (usually `C:\Windows`)
- `C:\Windows\System32\` - core OS folder, contains critical executables
- `C:\Windows\System32\control.exe /name Microsoft.Troubleshooting` - open Troubleshooting

## Security & Permissions
- **Properties → Security** - manage file/folder permissions
- **User Account Control (UAC) Settings** - manages privilege elevation level
- **View Advanced System Settings** - system properties, environment variables
- **Startup and Recovery** - configure crash dump file settings

## CMD Commands
| Command | Description |
|---------|-------------|
| `hostname` | Show device name |
| `whoami` | Show current user |
| `ipconfig` | Show network address settings |
| `ipconfig /all` | Show detailed network info (MAC, DNS, DHCP) |
| `netstat` | Show protocol statistics and active connections |
| `netstat -an` | Show all connections and listening ports |
| `net` | Manage network resources |
| `net help <command>` | Help about specific net command (e.g. `net help user`) |
| `cls` | Clear terminal window |
| `/?` | Manual for any command (e.g. `ipconfig /?`) |

## Active Directory (PowerShell)
```powershell
# Reset user password
Set-ADAccountPassword sophie -Reset -NewPassword (Read-Host -AsSecureString -Prompt 'New Password') -Verbose

# Force password change at next login
Set-ADUser -ChangePasswordAtLogon $true -Identity sophie -Verbose

# Force Group Policy update immediately
gpupdate /force
```

## Active Directory Concepts
- **OUs (Organizational Units)** - containers for users/computers, used to apply Group Policies
- **Group Policy Management** - apply settings and restrictions to OUs
- **Delegation** - grant specific users admin rights over an OU without full admin access
- Best practice: **separate workstations and servers** into different OUs for targeted policy control

## Key Security Concepts
- **Registry** - hierarchical database storing configuration for OS and applications, target for malware persistence
- **UAC** - prompts for confirmation when apps request elevated privileges, prevents silent installs
- **Startup folder** (`shell:startup`) - programs here run automatically on login, common malware persistence location

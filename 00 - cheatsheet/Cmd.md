# CMD & PowerShell & Linux Shells Cheatsheet

## CMD - System Info
| Command | Description |
|---------|-------------|
| `set` | Check environment variables and PATH |
| `ver` | Show Windows version |
| `systeminfo` | Detailed system information (OS, RAM, hotfixes) |
| `cls` | Clear terminal window |
| `driverquery` | List all installed drivers |
| `sfc /scannow` | Scan system files for corruption |
| `chkdsk` | Check file system for errors |

## CMD - Network
| Command | Description |
|---------|-------------|
| `ipconfig` | Show network information |
| `ipconfig /all` | Detailed network info (MAC, DNS, DHCP) |
| `ping <target>` | Check if network server is reachable |
| `tracert <target>` | Track the network route to target |
| `nslookup <target>` | Show IP address of domain |
| `netstat -abon` | Current connections, listening ports, owning process |

## CMD - File System Navigation
| Command | Description |
|---------|-------------|
| `cd` | Show current directory |
| `cd <directory>` | Change directory |
| `cd ..` | Go up one level |
| `dir` | List child directories |
| `dir /a` | List including hidden directories |
| `dir /s` | List all files in current directory recursively |
| `tree` | Tree representation of files and folders |
| `mkdir` | Create directory |
| `rmdir` | Delete directory |

## CMD - File Operations
| Command | Description |
|---------|-------------|
| `type <file>` | View file content |
| `more <file>` | View larger file (paginated) |
| `copy <file> <new_file>` | Copy a file |
| `copy *.md` | Copy all files with .md extension |
| `move <file> <location>` | Move a file |
| `del <file>` | Delete a file |

## CMD - Processes
| Command | Description |
|---------|-------------|
| `tasklist` | List running processes |
| `tasklist /FI "imagename eq sshd.exe"` | Filter processes by name |
| `taskkill /PID <task_id>` | Kill a process by PID |
| `taskkill /IM <name> /F` | Force kill a process by name |

---

## PowerShell - Basics
| Command | Description |
|---------|-------------|
| `Get-Command` | List all available commands |
| `Get-Command -CommandType "Function"` | List only functions |
| `Get-Help <cmdlet>` | Help about a command |
| `Get-Help <cmdlet> -Examples` | Show usage examples |
| `Get-Alias` | List available aliases (e.g. `ls` = `Get-ChildItem`) |

## PowerShell - Modules
| Command | Description |
|---------|-------------|
| `Find-Module -Name "PowerShell*"` | Search online repositories for module |
| `Find-Module -Name "Remove*"` | Search with wildcard |
| `Install-Module -Name "PowerShellGet"` | Install a module |

## PowerShell - File System
| Command | Description |
|---------|-------------|
| `Get-ChildItem` | List all subfolders and files |
| `Get-ChildItem -Path <path>` | List at specific path |
| `Set-Location <path>` | Change directory |
| `New-Item -Path <path> -ItemType <type>` | Create file or folder |
| `Remove-Item -Path <path>` | Delete an item |
| `Copy-Item -Path <path> -Destination <dest>` | Copy an item |
| `Move-Item -Path <path> -Destination <dest>` | Move an item |
| `Get-Content -Path <path>` | Show content of a file |

## PowerShell - Piping & Filtering
```powershell
# Pipe output of one command into another
Get-ChildItem | Sort-Object Length

# Filter by property
Get-ChildItem | Where-Object -Property "Extension" -eq ".txt"

# Comparison operators:
# -eq   equal
# -ne   not equal
# -gt   greater than
# -ge   greater or equal
# -lt   less than
# -le   less or equal
# -like wildcard match (e.g. "ship*")

# Select specific properties
Get-ChildItem | Select-Object Name, Length
Get-ChildItem | Select-Object -First 1

# Search for pattern in file
Select-String -Path ".\file.txt" -Pattern "hat"
```

## PowerShell - System Info
| Command | Description |
|---------|-------------|
| `Get-ComputerInfo` | Detailed computer information |
| `Get-LocalUser` | List all local user accounts |
| `Get-NetIPConfiguration` | Network interface information |
| `Get-Process` | List all running processes |
| `Get-Service` | List all services and their status |
| `Get-NetTCPConnection` | Display current TCP connections |
| `Get-FileHash -Path <file>` | Get file hash (useful for integrity checks) |
| `Get-Item -Path <file> -Stream *` | Show all file streams (ADS detection) |

## PowerShell - Remote Execution
```powershell
# Run command on remote computer
Invoke-Command -ComputerName RoyalFortune -ScriptBlock { Get-Service }

# General syntax
Invoke-Command -ComputerName <name> -ScriptBlock { <command> }
```

## PowerShell - Active Directory
```powershell
# Reset user password
Set-ADAccountPassword sophie -Reset -NewPassword (Read-Host -AsSecureString -Prompt 'New Password') -Verbose

# Force password change at next login
Set-ADUser -ChangePasswordAtLogon $true -Identity sophie -Verbose

# Force Group Policy update
gpupdate /force
```

---

## Linux - Shell Basics
| Command | Description |
|---------|-------------|
| `pwd` | Show current directory |
| `cd <directory>` | Change directory |
| `ls` | List subdirectories |
| `cat <file>` | Show content of a file |
| `grep <pattern> <file>` | Search for pattern in file |

## Linux - Shell Management
| Command | Description |
|---------|-------------|
| `echo $SHELL` | Check current shell |
| `cat /etc/shells` | List all available shells |
| `zsh` | Switch to zsh shell |
| `chsh -s /usr/bin/zsh` | Change default shell permanently |

## Linux - Bash Scripting
```bash
#!/bin/bash          # shebang - must be first line of script
chmod +x script.sh   # give execution permission
./script.sh          # run the script
nano script.sh       # create/edit a script

# For loop example
for i in {1..10}; do
    echo $i
done
```

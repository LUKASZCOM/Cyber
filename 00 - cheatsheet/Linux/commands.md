# Linux Fundamentals - TryHackMe Notes

## Recon Tools
- `dirb` - find hidden URLs/directories by brute-forcing
- `dirb http://target.com /usr/share/wordlists/dirb/common.txt`
- Passive recon - don't touch the target (Shodan, VirusTotal) - target doesn't know
- Active recon - directly scan the target (dirb, nmap) - leaves traces in logs

## Monitoring
- **Shodan** - monitors what has public connection
- **VirusTotal** - checks files/URLs/domains for being flagged
- **CVE** - identifies weak parts (each identified breach)

## SSH / Remote Access
- `ssh user@IP` - connect to remote machine
- `su user2` - switch to another user (more privileges)

## Linux Basics
- `man <command>` - documentation
- `echo "..."` - returns text we provide
- `whoami` - returns current logged in user
- `pwd` - shows full path to current directory

## File System Navigation
- `ls` - list folders
- `ls -a` - list all folders (including hidden)
- `ls --help` - help with ls
- `ls -lh` - show permissions and owner
- `cd` - change directory
- `cat` - show content of file
- `find -name <file/*>` - find path to file
- `grep "81.143.211.90" access.log` - search for string in file
- `grep -R "PRETTY_NAME" /etc/` - search recursively in whole directory

## Operators
- `&` - run command in the background
- `cmd1 && cmd2` - run cmd2 after cmd1 completes
- `echo hey > welcome` - write "hey" to file "welcome" (overwrite)
- `echo hello >> welcome` - append "hello" to end of file "welcome"

## File Management
- `touch` - create file
- `mkdir` - create folder
- `cp` - copy file/folder
- `mv` - move file/folder
- `rm` - remove file/folder
- `file` - show type of file

## Permissions
```
ls -lh - show permissions and owner
Format: Owner / Group / Others - 3/3/3 bits each
- read    = 4
- write   = 2
- execute = 1
Example: 7 = read+write+execute, 5 = read+execute
```

## Key Directories
- `/etc` - store system configuration files
- `/var` - store data frequently accessed or changed (logs, databases)
- `/root` - home directory for root user
- `/tmp` - store temporary data needed only once or twice

## File Editing & Transfer
- `nano <file>` - edit a file
- `wget <http://address>` - download file from URL
- `scp important.txt ubuntu@192.168.1.30:/home/ubuntu/transferred.txt` - transfer file from local to remote host

### Serving files over HTTP
```bash
# Terminal 1 - start HTTP server
python3 -m http.server

# Terminal 2 - download file from that server
wget http://MACHINE_IP:8000/myfile
```

## Processes
- `ps` - list running processes (current user)
- `ps aux` - list all processes including system
- `top` - live view of running processes
- `kill <PID>` - terminate a process
- `echo "Hi THM" &` - run in background, returns process ID
- `fg` - foreground a background process

### Kill signals
- `SIGTERM` - kill process but allow cleanup
- `SIGKILL` - kill process immediately, no cleanup
- `SIGSTOP` - pause/stop a process

### Services
- `systemctl [option] [service]` - manage services
  - options: `start` / `stop` / `enable` / `disable` / `status`
  - enable = start automatically on boot

## Process Automation (Crontabs)
- `crontab -e` - edit cron jobs
- Format: `MIN HOUR DOM MON DOW CMD`
- Example: `0 */12 * * * cp -R /home/cmnatic/Documents /var/backups/` - backup every 12 hours
- `@reboot /script.sh` - run script on every system startup

## Package Management
- `apt update` - refresh package list
- `apt install <name>` - install program
- `apt remove <name>` - remove program
- `add-apt-repository` - add third-party repository
- `add-apt-repository --remove ppa:PPA_Name/ppa` - remove repository
- `dpkg` - low-level software installer
- `/etc/apt/sources.list.d/` - folder containing repository sources

### GPG Keys
GPG key - digital signature from software developers, verifies that a package is authentic and hasn't been tampered with. Must be trusted before installing from third-party repos.

## Logs
- `/var/log/apache2/access.log` - web server visitor log
- `/var/log/apache2/error.log` - web server error log
- `access.log.1` - previous rotated log (when current is inaccessible)
- `access.log.2.gz` - older logs, compressed to save space

### Apache log format
```
IP - - [date] "METHOD /file HTTP/1.1" response_code size "browser"
```

### HTTP response codes
- `200` - OK (success)
- `403` - Forbidden (no permission)
- `404` - Not Found

### Log rotation
System automatically manages log size:
`access.log` → (after rotation) → `access.log.1` → `access.log.2.gz` → (deleted)
Important for incident response: if an attack happened last week, check `access.log.1` not `access.log`


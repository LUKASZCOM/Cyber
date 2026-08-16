properties setting - Properties -> Security 
%windir% - system variable
system32 - folder with OS
lusrmgr.msc - Local User and Group Management 
msconfig - system configuration
shell:startup - autostart apps
View advanced system settings - system properties, settings
Startup and Recovery - crash dump file
C:\Windows\System32\control.exe /name Microsoft.Troubleshooting - troubleshooting
User Account Control Settings - manages control level
compmgmt.msc - computer controling
perfmon - performance monitoring
msinfo32.exe - system information
resmon - resources monitor

CMD commands:
- hostname - device name
- whoami - user
- ipconfig - network adress settings
- /? - manual for command
- cls - clear window
- netstat - protocol statistics
- net - manage network resources
- net help <user> - help about user
- regedit - registry editor - configuration system for users


Delegation:
PS C:\Users\phillip> Set-ADAccountPassword sophie -Reset -NewPassword (Read-Host -AsSecureString -Prompt 'New Password') -Verbose
PS C:\Users\phillip> Set-ADUser -ChangePasswordAtLogon $true -Identity sophie -Verbose

Separate workstations and servers
Group policy maganement - OUs policies
PS C:\> gpupdate /force

# Wdedk 1 Day 1 - Linux Filesystem & Navigation  
## Commands leanred 
- pwd - print working directory, shows where you are 
- ls - list files in current directory 
- ls  -la - list all files including hidden, with full details 
- cd - change directory 
- cat - read and print file contents 
-head -N - show first N lines of output 
- tail -N - show last N lines of output 
- mkdir -p - create directory and any missing parents

## Key directories 
- /etc - system config files, owned by root, controls system behaviour
- /var/log - system logs, evidence trail for securtity investigations 
- /var/tmp - world-writtable with sticky bits (drwxrwxrwt)
 - /bin - system binaries must be owned by root only
- tmp - temporary files, cleared on reboot, target for attcakers 

## Permissio string structure 
d  rwx  rwx  rwx
|   |    |    |
|   |    |  others
|   |   group 
| owner 
file type (d=directory, -=file, l=symlink)

## Security concepts from today
- Principle of least privilege - only minimum permissions needed 
- Binary hijacking - replacing /bin commands with malicious versions 
- Sticky bit (t) - anyone can write but only owner can delete their files 
- Log rotation - logs compresssed and renamed nightly, 7 days retained
- PCI-DSS requires 12 months log retention, 3 months immediately available 
- Gaps in logs are as suspicious as the logs themselves 

## Finance background link 
- /var/audit is like a financial audit trail - restricted access, tamper-evident
- Log analysis = transaction forensics, same methodology different data
- Missing log entries = missing transaction records, both are red flags 
-PCI-DSS lg retention mirrors financial record-keeping requirements 

## Red flags to watch for in audits 
- drwxrwxrwx without sticky bit = world-writable, dangerous
 - Files in /bin not owned by root = potential binary hijacking 
- Gaps in log timestamps = possible log tampering 
- Unexpected entries in /etc/shells = potential backdoor shell

# Week 1 Day 1 - Linux Filesystem & Navigation

## Commands learned
- pwd - print working directory, shows current location
- ls - list visible files in current directory
- ls -la - list all files including hidden, with full details
- cd - change directory
- cd ~ - go home from anywhere
- cd .. - move one level up
- cat - read and print file contents
- head -N - show first N lines of output
- tail -N - show last N lines of output
- mkdir -p - create directory and any missing parents
- whoami - print current username
- id - show full identity: uid, gid, and all groups
- echo $PWD - print current directory from shell variable
- echo $HOME - print home directory path (never changes)

## Absolute vs relative paths
- Absolute path starts with / - works from anywhere (e.g. /etc/hosts)
- Relative path starts without / - depends on current location (e.g. cd etc)
- .. means parent directory
- . means current directory
- ~ always means home directory

## Permission string structure
- Format: [type][owner][group][others]
- d = directory, - = file, l = symlink
- r = read (4), w = write (2), x = execute (1), - = not granted (0)
- Add each block to get octal: rwx=7, r-x=5, rw-=6, r--=4, ---=0

## Common permission numbers
- 700 = rwx------ (private, owner only)
- 755 = rwxr-xr-x (directories, public executables)
- 644 = rw-r--r-- (regular files, configs)
- 600 = rw------- (private files, SSH keys)
- 777 = rwxrwxrwx (red flag - world writable)

## Key directories
- /bin - system binaries (ls, cat, cd) - must be owned by root only
- /etc - system configuration files - controls all system behaviour
- /var/log - system logs - evidence trail for security investigations
- /var/tmp - world-writable with sticky bit (drwxrwxrwt)
- /tmp - temporary files, cleared on reboot, target for attackers
- /Users - home directories for all user accounts
- /dev - device files - disks, terminals, random number generators

## Critical /etc files
- /etc/passwd - user accounts, format: username:password:uid:gid:desc:home:shell
- /etc/shadow - password hashes (Linux only, root-only access)
- /etc/hosts - hostname to IP mappings, checked before DNS
- /etc/shells - valid login shells, SSH refuses shells not listed here
- /etc/sudoers - who can run sudo and what commands
- /etc/ssh/sshd_config - SSH server configuration

## /etc/hosts attack
- Checked before DNS - overrides internet DNS entirely
- If compromised: attacker adds "127.0.0.1 bankofamerica.com"
- Every visit to that domain goes to attacker's fake page
- Called DNS hijacking via hosts file
- Enables phishing, credential theft, traffic interception

## /etc/passwd structure
username:password:uid:gid:description:home_directory:shell
- password field shows * on macOS (stored elsewhere)
- uid 0 = root always
- /usr/bin/false as shell = account cannot login interactively
- /var/empty as home = sterile, nothing stored

## Security concepts
- Principle of least privilege - only minimum permissions needed
- Binary hijacking - replacing /bin commands with malicious versions
- Private key theft - copying SSH private key to impersonate owner
- DNS hijacking - modifying /etc/hosts to redirect domains
- Sticky bit (t) - anyone can write but only owner can delete their files
- Log rotation - logs compressed and renamed nightly, 7 days retained
- PCI-DSS requires 12 months log retention, 3 months immediately available
- Gaps in logs are as suspicious as the logs themselves

## Finance background link
- /var/audit = financial audit trail - restricted access, tamper-evident
- /etc = policy documents - only authorised parties can modify
- Log analysis = transaction forensics, same methodology different data
- Missing log entries = missing transaction records, both are red flags
- PCI-DSS log retention mirrors financial record-keeping requirements
- File integrity monitoring = reconciliation controls in finance

## Red flags in audits
- drwxrwxrwx without sticky bit = world-writable, dangerous
- Files in /bin not owned by root = potential binary hijacking
- Gaps in log timestamps = possible log tampering
- Unexpected entries in /etc/shells = potential backdoor shell
- /etc/hosts modified unexpectedly = DNS hijacking attempt
- New accounts in /etc/passwd = potential backdoor user
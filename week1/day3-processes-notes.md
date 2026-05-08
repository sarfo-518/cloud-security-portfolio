# Week 1 Day 3 - Processes and Services

## Commands learned
- ps - show processes in current terminal session
- ps aux - show ALL processes on the system (all users, all terminals)
- ps aux | grep name - filter process list by name
- grep -v grep - remove grep itself from results
- kill PID - send SIGTERM (signal 15) to process, polite stop
- kill -9 PID - send SIGKILL, cannot be ignored, immediate termination
- sleep N & - run a command in background, returns prompt immediately

## Key concepts

### What is a process
Every running program is a process. Each gets a unique PID assigned by the kernel.
PID 1 = launchd (macOS) or systemd (Linux) - first process, parent of all others.

### ps aux columns
- USER - which account owns the process
- PID - unique process ID
- %CPU - CPU usage percentage
- %MEM - memory usage percentage
- TT - terminal attached to (?? = background, no terminal)
- STAT - process state (S=sleeping, R=running, Ss=session leader)
- STARTED - when it started
- TIME - total CPU time consumed
- COMMAND - full command that launched it

### Kill signals
- SIGTERM (15) - polite request to stop, process can clean up
- SIGKILL (9) - immediate kill, cannot be caught or ignored
- Use kill -9 during incident response to stop malicious processes immediately

### Background vs foreground
- command = runs in foreground, blocks terminal
- command & = runs in background, prompt returns immediately
- Ctrl+C = interrupt and stop foreground process

## Security observations from today
- PID 1 (launchd) owned by root - if compromised, entire system is compromised
- _mysql runs as its own account - least privilege for services
- _windowserver runs as its own account - isolated from root and user
- Unrecognised process running as root at 3am = first indicator of compromise

## Incident response process checklist
1. ps aux - see everything running
2. Look for unrecognised processes
3. Check what user they run as
4. Check when they started (middle of night = suspicious)
5. kill -9 PID - stop malicious process immediately
6. Investigate the binary path in COMMAND column

## Finance background link
- Process isolation = segregation of duties in finance
- Each service running as its own account = no single account has unlimited access
- kill -9 = emergency freeze on a suspicious transaction

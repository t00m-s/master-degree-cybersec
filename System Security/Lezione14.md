# Operating System security
A program may have a vulnerability, that is a possibility.
However, a operating system has to try to guarantee that nothing bad will happen in that case.
The idea is to have the security as a hardening process:
- Whitelist approved applications
- Patch non default applications (*the ones that you can download* )
- Patch the operating system itself, since it's still code that is running it could have vulnerabilities itself.
- Restrict admin privilege (**least privilege principle**).
## Layers of security
- Physical hardware
- Operating system
  Code that runs on bare metal.
- Applications and utilities
  Those interact with the operating system APIs
## Steps for OS Security
### Security planning
Should be done from the beginning, to maximize security and minimize extra costs (adding security after is more expensive and probably harder to do).
List of things that should be planned:
- Purpose of the system
- Categories of users
- Authentication flow and methods
- Admin location and mode (local - ssh)
- Additional security mechanisms (firewall, logger, $\dots$)
### System installation
Should be done in a isolated environment, the most vulnerable state of the system.
If a connection is necessary it should be towards a **verified** site.
Secure boot is a technology that helps with BIOS tampering, limiting the boot media to an authorized one to prevent tampering with the hypervisior / bypass of access control via external boot drives.
During the system installation adding encryption should be preferable to add a layer of protection against tampering.
### Trusted code and patching
Drivers should be handled with care, since they could be malware and drivers usually have kernel level privilege.
Security patches and updates should be regularly installed; however automatic updates are not a preferred choice since they could break applications (*think about arch linux*).
### Unnecessary services and access control
Balance security and usability, additional unnecessary software may be an attack vector.
Keep in mind that **not installing software** and **removing/disabling** software are not truly the same thing, an attacker could re-install software.
Access control should be implemented, either via 
[[System Security/Lezione7#Discretionary Access Control (DAC)|DAC]], [[System Security/Lezione7#Role-based Access Control|RBAC]] or [[System Security/Lezione7#Mandatory Access Control (MAC)|MAC]].
Administrative privileges should be restricted to:
- Few users.
- Every administrative action has to be logged.
- Use those privileges only when necessary.
### Additional security
- Anti-virus software
- Host-based firewall, IDS
  Filters connections and monitors traffic.
- Whitelisting system applications to prevent execution of malware
- Security tools to scan configurations/ vulnerabilities
### Application security
- Default configuration should be reviewed for security 
- Apply **minimum privilege** when possible.
### Logging
Necessary for obtaining informations about what happened, either normal activity or malicious activity.
In the second case it's crucial for recovery and security assessment about what went wrong.
What to log depends on the [[#Security planning|security planning]] phase.
- Log rotation is necessary when there's a huge number of logs. That is the practice of comppressing, archiving and deleting log files once certain conditions have been met (size, date, $\dots$)
- Automation of log analysis is ideal due to the volume of the logs, a manual analysis is most likely unreliable and hard to do.
### Backups
Making copies of data at regular intervals, so that in the event of a recovery (breach, disaster, etc $\dots$) as few data as possible is lost. Often data is backed up for legal reason. (*think about disaster recovery*)
# Case study
## Linux
- Automatic system updates via package managers
- Configuration in dotfiles or /etc/ folder
- Permissions with the rwx triad.
- User information in /etc/passwd,shadow,group
- Authentication with pluggable authentication module (PAM)
- Login can be disabled if not necessary
- SUID programs should be limited (SUID gives the program the same users as the creator)
- Linux has a tcp wrapper with the /etc/hosts.allow/deny files
- Logs are managed with **syslogd**, **logrotate** manages log rotation.
- chroot jail is a feature that sets the root filesystem of a service. This hides the real root file system (e.g. chroot /srv/ftp/ sets the root directory as /srv/ftp, the user will then see that directory as his /)
- metasploit, nmap, $\dots$ as security tools
- [[System Security/Lezione7#Mandatory Access Control (MAC)|MAC]] implementations such as AppArmor and SELinux
## Windows
- Windows update
- Configuration in registry, a key-value database.
- fuck windows, not writing anything else (se lo becco all'esame porcono, mark my words).
# Virtualization
## Hypervisors
Software between the hardware and virtual machines, provides abstraction of physical resources; enables a machine to run multiple VMs in the same "metal".
### Type 1
"Runs before the OS", **native virtualization**.
### Type 2 
"Runs inside the OS", **hosted virtualization**.

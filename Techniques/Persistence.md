We should accomplish persistence several ways if possible, while sometimes leaving false IOCs, assisting us in [[Evasion|Evading]] detection. 
## Persistence via C2 Infrastructure

The C2 implant of choice for CU at the time of writing is [[Sliver C2]]. You can find a whole host of other options in the C2Matrix here: https://docs.google.com/spreadsheets/d/1b4mUxa6cDQuTV2BPC6aA-GR4zGZi0ooPYtBe4IgPsSc/edit#gid=0. This is a publicly available resource that compares C2 infrastructures against each other. If evasion becomes an absolute necessity in the future, or Sliver's feature count becomes insufficient, the author recommends rolling a custom [[Mythic]] agent, or building our own custom C2 infrastructure using existing techniques.

[[MSFVenom]] also contains functionality for binding malware to legitimate executables. However, this must be done in conjunction with [[Evasion]] as all MSFVenom payloads and TTPs are well signatured. 
### Persistence via LOL
- Linux
	- Cron jobs
	- Install and enable new service
	- Malicious user acct or ssh keys
- Windows
	- Registry Run Keys
	- Scheduled Tasks
		- Can delete attribute SD from task at HKLM\\SOFTWARE\\Microsoft\\Windows NT\\CurrentVersion\\Schedule\\Tree\\\<TASK\> to hide the running task from `schtasks`.
	- Startup Folder
	- Malicious user acct
		- Administrator User
			- If NOT:
				- Backup Operators && Remote Management Users member can export HKLM\\system and HKLM\\sam to PTH with [[Evil-WinRM]]. This can also be accomplished by editing config.inf with [[secedit]] directly and adding the user to privileged groups and assigning privileges to the user directly via the GUI. This prevents the new groups from appearing in a user summary. TODO: Finish this with more details
	- DLL Hijacking
	- Poisoning Shortcuts
	- Backdoor Applications
		- [[MSFVenom]] has functionality for this.
	- Replace Default Applications for File types
		- HKEY_CLASSES_ROOT???
	- Malicious Services
		- Replace the binPath property of an existing Windows service with your implant to avoid creating a new service. Simple commands can also be used as binPath, meaning `net user redteam password /add` is permissible. If you plan to use an implant as a service make sure to compile as `exe-service` with [[MSFVenom]].

## Domain Persistence
### Credentials
You can acquire hashes of users using [[Mimikatz]]'s DCSync functionality for every user. This will grant access to the krbtgt account for golden tickets, etc. 

### Tickets
Golden and Silver Tickets are incredibly useful, and will grant persistence as well. The are generated most easily with [[Rubeus]] and [[Mimikatz]]. 

### Certificates

> [!error] Danger
> If you are generating a CA to have persistence, you are making blue team rebuild the domain to get you out. Only do this in nation-state sims and competitions where the domain does NOT have to be reused. In a penetration test, this is so far overkill you will not be invited back. 

[[Mimikatz]]

### SID History


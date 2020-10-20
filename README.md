# Windows-Administration-and-Hardening
We will create domain-hardening GPOs and some PowerShell fundamentals.

# Task 1: Create a GPO: Disable Local Link Multicast Name Resolution (LLMNR)
For this first task, you will investigate and mitigate one of the attack vectors that exists within a Windows domain.


Read about LLMNR vulnerabilities in the the MITRE ATT&CK database.


MITRE is one of the world's leading organizations for threat intelligence in cybersecurity.


MITRE maintains the Common Vulnerabilities and Exposures database, which catalogs officially known exploits.


It also maintains this MITRE ATT&CK database, which catalogs attack methods and signatures of known hacking groups.




Local Link Multicast Name Resolution (LLMNR) is a vulnerability, so we will be disabling it on our Windows 10 machine (via the GC Computers OU).
A few notes about LLMNR:


LLMNR is a protocol used as a backup (not an alternative) for DNS in Windows.


When Windows cannot find a local address (e.g. the location of a file server), it uses LLMNR to send out a broadcast across the network asking if any device knows the address.


LLMNR’s vulnerability is that it accepts any response as authentic, allowing attackers to poison or spoof LLMNR responses, forcing devices to authenticate to them.


An LLMNR-enabled Windows machine may automatically trust responses from anyone in the network.


Turning off LLMNR for the GC Computers OU will prevent our Windows machine from trusting location responses from potential attackers.

# Task 2: Create a GPO: Account Lockout
For security and compliance reasons, the CIO needs us to implement an account lockout policy on our Windows workstation. 
An account lockout disables access to an account for a set period of time after a specific number of failed login attempts. 
This policy defends against brute-force attacks, in which attackers can enter a million passwords in just a few minutes.

# Task 3: Create a GPO: Enabling Verbose PowerShell Logging and Transcription
PowerShell is often used as a living off the land hacker tool. This means:

Once a hacker gains access to a Windows machine, they will leverage built-in tools, such as PowerShell and wmic, as much as possible to achieve their goals while trying to stay under the radar.

So why not just completely disable PowerShell?


Many security tools and system administration management operations, such as workstation provisioning, require heavy use of PowerShell to set up machines.


Best practices for enabling or disabling PowerShell are debated. This often leads to the solution of allowing only certain applications to run. These setups require a heavy amount of configuration using tools such as AppLocker.


This is why we're going to use a PowerShell practice that is recommended regardless of whether PowerShell is enabled or disabled: enabling enhanced PowerShell logging and visibility through verbosity.


This type of policy is important for tools like SIEM and for forensics operations, as it helps combat obfuscated PowerShell payloads.

# Task 4: Create a Script: Enumerate Access Control Lists

Create a PowerShell script that will enumerate the Access Control List of each file or subdirectory within the current working directory.

# Bonus: Verify Your PowerShell Logging GPO
For this task we'll test and verify that our PowerShell logging GPO is working properly.



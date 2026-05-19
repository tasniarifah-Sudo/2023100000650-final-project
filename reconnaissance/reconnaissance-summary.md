 Reconnaissance Summary

Room: Active Reconnaissance (TryHackMe)

Objective Perform active reconnaissance against the target host to identify open ports, running services, and potential attack vectors as part of the external penetration test simulation for PosBuzz Retail Solutions.

Methodology Active reconnaissance was conducted using Nmap, the industry-standard port scanner, with service version detection and vulnerability scripts enabled.

Primary command used:

nmap -sV --script vuln <TARGET_IP>

Key Findings

Port Scan Results

Port State Service Version

135/tcp Open msrpc Microsoft Windows RPC

139/tcp Open netbios-ssn Microsoft Windows NetBIOS

445/tcp Open microsoft-ds Windows 7–10 SMB (Workgroup: WORKGROUP)

3389/tcp Open tcpwrapped Remote Desktop Protocol (RDP)

Total open ports under 1000: 3 (ports 135, 139, 445)

Host OS: Windows (identified as JON-PC)

MAC Address: 02:CB:77:08:95:55

Vulnerability Detection

The Nmap vulnerability script (smb-vuln-ms17-010) confirmed the target is VULNERABLE to:

MS17-010 (EternalBlue) — Remote Code Execution vulnerability in Microsoft SMBv1

CVE: CVE-2017-0143

Risk Factor: HIGH

Disclosure Date: 2017-03-14

Security Impact

The presence of unpatched SMBv1 with MS17-010 allows an unauthenticated attacker to execute arbitrary code remotely with SYSTEM-level privileges. This vulnerability was exploited in real-world attacks including WannaCry and NotPetya ransomware campaigns, resulting in widespread damage globally.

Remediation Recommendations

Disable SMBv1 immediately — it is a legacy protocol with no legitimate modern use case.

Apply Microsoft Security Bulletin MS17-010 patch (KB4012212 for Windows 7).

Block inbound SMB (port 445) at the network perimeter firewall.

Disable RDP if not required, or restrict access via VPN and enforce Network Level Authentication (NLA). Implement regular vulnerability scanning to catch unpatched services proactively.

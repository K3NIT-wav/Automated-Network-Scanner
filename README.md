# Automated Network Recon and Vulnerability Scanning Project

This is one of the hands-on project I have done. This project was carried out in order to learn and demonstrate network reconnaissance and security scanning using Nmap commands. This project documents my practical exploration of Nmap, the industry-standard network security tool, and its wide range of capabilities. For this project, I started completely from scratch - installing the necessary software on macOS then  progressed to performing host discovery, port scanning, decoy scanning, and basic automated vulnerability assessment on my own home network.

### Disclaimer

This project was conducted solely on my own personal, private network for educational purposes. I am 100% aware that scanning networks without permission is illegal and unethical.

## The objectives were:

- Learn the end-to-end process of setting up a security tooling environment on macOS (using Terminal).
- Understand the fundamental concepts of network reconnaissance.
- Execute and interpret various Nmap scan types.
- Document the process and findings in a professional manner.

### Installation & Setup

The first challenge was installing Nmap on macOS, which requires a package manager called Homebrew. I initially attempted to run the nmap command on the Terminal bash, however, the bash would return with "command not found". I then figured, I needed to install it onto my system using a Homebrew command, which also returned with the same error. I ultimately found out that I had to start from scratch, which began with installing Homebrew in order to use their commands to then install 'Nmap'.

1.  **Install Homebrew:** Copied the installation command from the official Homebrew GitHub repository and ran it in the terminal to install the package manager.
2.  **Install Nmap:** Used Homebrew to install Nmap with the command: `brew install nmap'.

### Scan Examples & Findings

Here are the key scans I performed and what I learned from them.

### 1. Host Discovery ('-sP')
**Command:** 'nmap -sP [home IP range]'

**Purpose:** To identify all active devices on my local network.

**What I Learnt:** I found out how simple and easy it is to successfully list the number of hosts (devices) connected to my network using the Nmap ping scan command. I also found out how long it takes to scan entire networks. For example, pressing the 'Enter' button whilst the command is still running will give you feedback on the status in which my terminal printed "Parallel DNS resolution of 4096 hosts. Timing: About 4.79% done; ETC: 03:31 (0:32:30 remaining)".

### 2. TCP Port Scan ('-sT', '-sS')
**Commands:**
- 'sudo nmap -sT -p 80,443 [target IP]' (Full Connect Scan)
- 'sudo nmap -sS -p 80,443 [target IP]'  (Stealth SYN Scan)

**Purpose:** To determine if specific ports (80 for HTTP, 443 for HTTPS) were open on a target device.

**Learning:** Discovered the difference between a loud, complete connection scan ('-sT') and a stealthier "half-open" scan (`-sS`) that doesn't complete the TCP handshake. In a complete connection scan, the target IP/host server is made aware of your connection with the 3rd and final step in the "3-way Handshake", which would be the ACK message. The ACK message comes after you request a connection with the target host, with a SYN request, followed by the host's SYN-ACK response/acknowledgment for your request. However, using the '-sS' switch means that your server does not complete the handshake with the 3rd step, thus remaining stealthy and incognito. 

- This knowledge and skill is essential for red-teaming and ethical hacking, which is what I take a liking to as well.

### 3. Decoy Scan ('-D')
**Command:** 'sudo nmap -sS -D [decoy IPs] [target IP]'

**Purpose:** To obfuscate the source of the scan by mixing my IP address with a decoy IP.

**What I Learnt:** The '-D' command stands for "decoy" and any decoy IP or IP range you insert afterwards will be used to send SYN requests to the target IP address, along with SYN requests coming from your actual host IP. This then creates a larger pool of IP sources of pings, which will be seen in a network traffic log. This makes it a little bit more difficult for someone, analysing the packet/log, to pinpoint the true source of the SYN flood.      

- I learnt a skill and now understand how attackers use this technique to hide their tracks and how security analysts must look for multiple sources in logs.
- Demonstrated privilege escalation using the 'sudo' command, which gives users temporary permissions.

### 4. Vulnerability Scanning ('--script vuln')
**Command:** 'sudo nmap --script vuln [target IP]

**Purpose:** To run a scan against a target to identify known vulnerabilities/CVE.

**What I Learnt:** Going on the Nmap official website, you can find all the script commands required to run individual scans against specific vulnerabilities. However, I figured out a way to automatically input all of those commands into a singular script, which is through using 'vuln' after '--script'. This created a scripted scan, which scanned the target IP for every vulnearbilty in the Nmap catalogue. 

- **Critical Finding:** The scan detected a **Slowloris Denial-of-Service (DoS) vulnerability** on my router. This is a significant finding that demonstrates the practical value of tools, such as Nmap.

- I learnt how important it is to keep up with the security posture at your home network, ensuring your systems and network security is updated and hardened as much as possible. I also discovered.

### 5. Service Version Detection ('-sV', '-sC')
**Command:** 'sudo nmap -sV -sC [target IP]'

**Purpose:** After finding an open port, you can find out those ports' current software and software version. These switches allow you to do so.

**What I Learnt:** I learnt that this command also returns a list of more ports that are open. For intance, I found out port 53 (version: Cloudflare Public DNS) is open. This command successfully identified the exact software and version numbers of services on my home network (e.g. Cloudflare). '-sC' provided additional useful information, such as HTTP headers, which reveals more about the server's configuration. 

- This is very important and could help analysts reduce the attack surface for threat actors by analysing the services and doing research on any known vulnerabilities tied with that specific service and version. 

## Conclusion

This project provided me with invaluable hands-on experience with fundamental cybersecurity tools and concepts. I progressed from unable to run 'nmap' to successfully identifying a potential vulnerability on my own network! This entire process taught me various command syntax as well as the underlying principles of network communication, reconnaissance, and the importance of ethical scanning. My skills and knowledge, such as attention to detail, critical thinking, technical problem-solving have been further developed through this project. Furthermore, my patience was also tested and improved due to the amount of errors and waiting times experienced during this fun project.

I also took the time to learn about more commands and switches (e.g. '-sA', '-sW', '-T0'), which were not used in this project but will definitely be used and tested **ethically** in future projects. One of the commands I look forward to trying is the '-T(0-4)' switches. This switch alters the speed or time interval between each scan. 

- **Hard Skills Used and Developed:**
  - Network Reconnaissance
  - Port Scanning
  - Scripting
  - Operational Security
  - Use of Nmap 
  

- **Tools and Technologies Used:**

  - macOS Terminal
  - Homebrew
  - Nmap
  - TCP/IP

### Thank you for taking your time to read this and I hope to hear from you.

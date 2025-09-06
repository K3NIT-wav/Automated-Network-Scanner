# Samples and Results

## Network Vulnerability Scanning

### Output Analysis:

From the results of entering the —script vuln command, I found a few red flags in my own home network.
- A critical finding was the Slowloris DoS Attack (CVE-2007-6750) vulnerability.
    - This technique has a severe impact on the network. It allows a single attacker to use minimal resources to open and hold multiple partial connections to the server, eventually consuming all available threads and preventing legitimate users from accessing the web management interface.
    - What I also found out about this vulnerability after some more research is that an attacker on the local network could leave the device's web-based configuration panel unreachable in which requires a reboot to restore functionality and limiting administrative access.

- After carrying this part of my homelab project out, I unfortunately (but also luckily) found out about my home network’s poor security posture, and I will now be making the right steps forward in correcting this and improving my security posture. This is strong (first-hand) evidence on the importance of auditing your security posture and implementing network security methods. 


## Service and Version Discovery

### Output Analysis:

From the results of entering the -sV -sC command, you can see a few interesting points of interest
- **Port 53** is open and is running Cloudflare’s well-known public DNS. This suggests that my router is configured with Cloudflare’s DNS (1.1.1.1) for all devices connected to the network, which is a solid security feature for browsing.
- **Port 80** is open. Port 80 is a web management port (HTTP), however, it is not the most secure option for that type of operation. 
    - Doing a bit of research on the names found under port 80, I discovered that “X-Frame-

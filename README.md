# Network Vulnerability Analysis and Defense Lab

## Overview
This project demonstrates end-to-end network security assessment, packet capture analysis, and host-based firewall defense using Kali Linux and Metasploitable2 within an isolated VirtualBox environment.

---

## Lab Architecture & Topology
* **Attacker Machine:** Kali Linux (`192.168.56.101`)
* **Target Machine:** Metasploitable2 (`192.168.56.102`)
* **Network Mode:** VirtualBox Host-Only Adapter (`192.168.56.0/24`)

---

## Summary of Tasks Executed

### Task 1: Network Discovery
* Verified ICMP connectivity between Kali Linux and Metasploitable2 using `ping`.
* Confirmed bidirectional routing on the isolated host-only subnet.

### Task 2: Port Scanning & Service Enumeration
* Performed deep TCP scanning using Nmap (`nmap -sV -sC -Pn 192.168.56.102`).
* Identified key open ports and legacy services including SSH (22), FTP (21), and HTTP (80).

### Task 3: Vulnerability Scanning
* Executed Nmap Scripting Engine (NSE) vulnerability detection (`nmap -Pn --script vuln 192.168.56.102`).
* Discovered unpatched legacy services and vulnerable web applications hosted on the target.

### Task 4: Packet Analysis with Wireshark
* **Credential Sniffing:** Filtered unencrypted FTP traffic (`ftp`) and successfully extracted plaintext login credentials (`msfadmin`).
* **SYN Flood Detection:** Simulated a SYN flood Denial-of-Service (DoS) attack using `hping3` and analyzed the high-volume TCP SYN packet patterns in Wireshark (`tcp.flags.syn == 1 and tcp.flags.ack == 0`).

### Task 5: Firewall Implementation (`iptables`)
* Configured host-based filtering rules on Metasploitable2 using `iptables`.
* Allowed SSH access (Port 22) while dropping incoming HTTP traffic (Port 80) using:
  `sudo iptables -A INPUT -p tcp --dport 80 -j DROP`
* Validated rule efficacy from Kali Linux using Nmap, confirming Port 80 shifted from `open` to `filtered`.

---

## Repository Files
* `reports/`: Raw Nmap text scan logs and vulnerability reports.
* `screenshots/`: Step-by-step visual evidence for all lab tasks.

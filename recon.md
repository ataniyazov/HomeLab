Reconnaissance is the initial step in a cyber attack where an attacker gathers information about the target. There are two types of reconnaissance: active and passive. Active reconnaissance involves sending probes to the target network or systems, while passive reconnaissance does not interact directly with the target, instead using third-party databases and eavesdropping on network traffic.

### Active Reconnaissance Methods
- **Host, Network, User, Group, Network Share, Web Page, Application, and Service Enumeration**
- **Packet Crafting**

### Passive Reconnaissance Methods
- **Domain Enumeration**
- **Packet Inspection**
- **Open-Source Intelligence (OSINT)**
- **Recon-ng**
- **Eavesdropping**

Active reconnaissance typically starts with minimal information and progressively gathers more through scanning. Techniques include DNS lookups, identifying technical and administrative contacts, social media scraping, and inspecting SSL certificate flaws. Certificate transparency helps gather information about an organization's subdomains and systems.

Security breaches can impact a company's reputation significantly. Attackers use various methods to gather information, including password dumps, file metadata, strategic search engine analysis, website archiving, and public source code repositories. Tools like h8mail and WhatBreach exploit breached data repositories, while ExifTool reveals metadata in files. Advanced search engine operators and website archiving provide historical views of websites. OSINT involves collecting and analyzing publicly available information using frameworks like Recon-ng. Shodan scans the internet for vulnerable hosts and exposed systems.

### Active Reconnaissance Techniques
- **Enumeration**: Gathering information about a target during penetration testing.
  - **Host Discovery**: Identifying if a host is online and responding.
  - **Port Scanning**: Enumerating services on target hosts using tools like Nmap.
    - **SYN Scan**: Sends a TCP SYN packet to determine if a service is listening.
    - **TCP Connect Scan**: Establishes a full TCP connection, possibly triggering IDS alarms.
    - **UDP Scan**: Enumerates services like DNS, SNMP, or DHCP.
    - **TCP FIN Scan**: Sends a FIN packet, with no response indicating an open port.

### Enumeration Techniques
- **Host Enumeration**: Scanning IP addresses using tools like Nmap or Masscan.
- **User Enumeration**: Collecting valid user lists, often manipulating the SMB protocol on Windows networks.
- **Group Enumeration**: Determining authorization roles by enumerating SMB groups.
- **Network Share Enumeration**: Identifying shared files, folders, and printers on a network.
- **Web Page/Application Enumeration**: Mapping web application attack surfaces.
- **Service Enumeration**: Identifying services on remote systems through port scanning.
- **Packet Crafting**: Using tools like Scapy for network reconnaissance.  

### Active Reconnaissance Tools  
- **Nmap** (Port scanning, host discovery)  
- **Masscan** (IP scanning)  
- **Scapy** (Packet crafting)  

### Passive Reconnaissance Tools  
- **Recon-ng** (OSINT framework)  
- **Shodan** (Internet-wide scanning for vulnerable hosts and systems)  
- **h8mail** (Exploring breached data repositories)  
- **WhatBreach** (Identifying breached accounts/data)  
- **ExifTool** (Extracting metadata from files)  

### Packet Inspection Tools  
- **Wireshark** (Network protocol analyzer)  
- **tshark** (Command-line network protocol analyzer)  
- **tcpdump** (Packet analysis and capture)  

### Information Gathering Tools  
- **SpiderFoot** (`spiderfoot -t 127.0.0.1:5001`) - Comprehensive reconnaissance tool  
- **GVM (Greenbone Vulnerability Manager)** (`gvm-start`) - GUI network scanner  

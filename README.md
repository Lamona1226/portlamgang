# Portlamgang
**PortLAMGang: Port Scanner, WAF Detection, and Censys Integration**

This project provides a Python-based tool for port scanning, WAF (Web Application Firewall) detection, and integration with Censys for gathering information about a target. It is designed to be modular, efficient, and easy to use.

**Features**

    Port Scanning:

        Scans a range of ports on a target IP or domain.

        Supports multi-threading for faster scans.

        Optionally uses nmap for service version detection.

    WAF Detection:

        Detects if a target is behind a WAF.

        Identifies specific WAF vendors (e.g., Cloudflare, Akamai).

        Works with both HTTP and HTTPS targets.

    Censys Integration:

        Scrapes data from Censys to gather information about open ports, services, OS, and network details.

        Supports searching by IP or domain.
# Installation
1.You should clone this repository using:
    
    git clone https://github.com/MajorRaccoon/RollerScanner.git
2.Install requirements:
    
    pip3 install -r requirements.txt
3.Run the script:
    
    python3 rollerscanner.py --target...
# Prerequisites

  .Python 3.x

  . Required Python libraries:
    

    pip install requests beautifulsoup4 colorama psutil

  .nmap (optional, for service version detection).

# Usage
1. Port Scanning

Run the script with the following command:


    python3 portlamgang.py --target <target> [options]

Options:

    --target: Specify the target IP or domain (required).

    --port or -p: Specify a port range (e.g., 1-1000) or individual ports (e.g., 80,443). Default: 1-65000.

    --nmapsv or -nsv: Enable service version detection using nmap.

    --http or --https: Specify the protocol for WAF detection.

    --censys or -c: Enable Censys data scraping.

Example:

    python3 portlamgang.py --target example.com --port 80,443 --nmapsv --https

2. WAF Detection

The script automatically detects WAFs if the --http or --https flag is used. It sends various attack vectors (e.g., XSS, SQLi) to identify WAFs.
Example Output:

    [*] The site https://example.com is behind Cloudflare WAF.
    [&] Number of requests: 5

3. Censys Integration

The script can scrape data from Censys to gather information about the target. Use the --censys or -c flag to enable this feature.
Example Output:


    [*] Protocol: HTTP is on port: 80
    [*] OS: Linux 4.15.0-112-generic
    [*] Network: AS12345 Example Network
    [*] Routing: BGP

# Modules
censys.py

This module interacts with Censys to gather information about a target. It supports:

    Searching by IP (SearchByIp).

    Searching by domain (SearchByDomain).

Example Usage:


    from modules.censys import SearchByIp, SearchByDomain
    
    # Search by IP
    SearchByIp("192.168.1.1")
    
    # Search by domain
    addresses = SearchByDomain("example.com")
    print(addresses)

wafmeow.py

This module detects WAFs by analyzing responses to various attack vectors. It uses the WAFW00F library under the hood.
Example Usage:


    from modules.wafmeow import wafsearch
    
    # Detect WAF for an HTTPS target
    wafsearch("example.com", "https://")

# Example Workflow

   1. Port Scan:
    
    python3 portlamgang.py --target example.com --port 1-1000 --nmapsv

   2. WAF Detection:
 

    python3 portlamgang.py --target example.com --https

   3. Censys Data Scraping:
  

    python3 portlamgang.py --target example.com --censys

| Switch | Example | Description
|:-----:|:-----|:----|
||nmap 192.168.1.1|Scan a single IP	
||nmap 192.168.1.1 192.168.2.1|Scan specific IPs
||nmap 192.168.1.1-254|Scan a range
||nmap scanme.nmap.org|Scan a domain
||nmap 192.168.1.0/24|Scan using CIDR notation
-iL|nmap -iL targets.txt|Scan targets from a file
-iR|nmap -iR 100|Scan 100 random hosts
--exclude|nmap --exclude 192.168.1.1|Exclude listed hosts






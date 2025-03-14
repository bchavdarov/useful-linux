# Useful commands in Linux to scan a local network

Scan a local network (assuming the subnet is 192.168.0.0/24)

`sudo nmap -sn 192.168.0.0/24`

Get IP Addresses, Hostnames, and MAC Addresses:

`sudo nmap -sP 192.168.0.0/24`

Use of arp-scan (Fastest). Install it first:

`sudo apt install arp-scan`

Then scan the network. *I prefer this method for common uses*:

`sudo arp-scan --localnet` 

If SSH access is enabled on a machine, check who is logged in:

`ssh user@192.168.0.X who`

or

`ssh user@192.168.0.X w`
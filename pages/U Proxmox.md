- # PROXMOX
  title:: U Proxmox
## Setup post installation
- 1. nano /etc/apt/sources.list
	- insert the following:
		- ---># not for production use
		  --->deb http://download.proxmox.com/debian bullseye pve-no-subscription
- 2. nano /etc/apt/sources.list.d/pve-enterprise.list
  comment out the following line:
	- ----># deb https://enterprise.proxmox.com/debian/pve bullseye pve-enterprise
- 3. at prompt 
  --->apt-get upgrade
  --->apt-get upgrade
- 4. remove other partitions (from other storage partitions)
	- --->fdisk /dev/sdx
	- then select p, then d (and select the partition/s to be removed)
	- then check with d again
	- etc until all are processed
- 4. nano /etc/default/grub
  5.
- 5. configure the storage
  5. make vlan aware
	- kk
- 7. n
  8.
- 9.
-
- 10. vlans
  nano /etc/network/interfaces
	-
- Reference: https://www.youtube.com/watch?v=GoZaMgEgrHw
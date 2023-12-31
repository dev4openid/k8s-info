- ## Backup To Remote Server
- https://linhost.info/2010/10/clone-and-restore-a-hard-drive-over-the-network-with-dd-gzip-and-openssh
- This command will copy, compress and send the image to the remote server.
  
  dd if=/dev/sdb | gzip -c –-fast | ssh user@ip ‘dd of=/home/user/sdb.img.gz’
  dd= if=/dev/sda | gzip -c --fast | ssh briandanks@192.168.1.103 'dd=/home/briandanks/proxmox-backup/prox-router.img.gz'
  
  Explanation: DD has been instructed to copy the drive /dev/sda. Gzip will be used for compression, "-c" means Write on standard output, keep original files unchanged, "--fast" mean Compress faster at the expense of high compression ratio. The image will then be transferred via OpenSSH using the provided user credentials to the user directory "/home/briandanks/proxmox-backup/".
  Notes: the backup image makes use of the ".gz" extension to indicate compression is being used. One could use "-1" instead of "--faster"
- ## Restore From Remote Server
  Restoring the image is not that different from the command used to backup the image.
  
  ssh user@ip ‘dd if=/home/user/sdb.img.gz’ | gunzip -1 - | dd of=/dev/sdb
  ssh briandanks@192.168.1.103 'dd=/home/briandanks/proxmox-backup/prox-router.img.gz' | gunzip --fast -c | dd of=/dev/sda
  
  Explanation: Using OpenSSH log in to the remote system where the image is stored and with DD pull the image. **Gunzip** will be used to decompress the image crated by Gzip. Once again DD will be in charged of writing the image to /dev/sdb.
- `rsync --help`
- https://www.tecmint.com/rsync-local-remote-file-synchronization-commands/
- https://www.howtogeek.com/451262/how-to-use-rclone-to-back-up-to-google-drive-on-linux/
- https://wiki.linuxquestions.org/wiki/Rsync_with_Google_Drive
- ```bash
  # !bash#!/bin/bash
  # rsync -r -b --backup-dir='~/zxcBackup' -A -X -o -g -u -t -p -v --dry-run /home/briandanks/gdrive_local/Learning  /home/briandanks/zxcBackup
                    
  rsync -r -b --backup-dir='~/zxcBackup' -A -X -o -g -u -t -p -v  /home/briandanks/gdrive_local/Learning  /home/briandanks/zxcBackup
  
  ```
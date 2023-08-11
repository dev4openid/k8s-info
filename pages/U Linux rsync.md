-
- https://www.tecmint.com/rsync-local-remote-file-synchronization-commands/
- ```bash
  # !bash#!/bin/bash
  # rsync -r -b --backup-dir='~/zxcBackup' -A -X -o -g -u -t -p -v --dry-run /home/briandanks/gdrive_local/Learning  /home/briandanks/zxcBackup
                    
  rsync -r -b --backup-dir='~/zxcBackup' -A -X -o -g -u -t -p -v  /home/briandanks/gdrive_local/Learning  /home/briandanks/zxcBackup
  
  ```
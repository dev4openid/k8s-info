- find config file at .config/rclone/rclone.conf
- pwd: 1Catinahat
- rclone  https://rclone.org
       https://wiki.linuxquestions.org/wiki/Rsync_with_Google_Drive
- rclone config
  rclone rcd --rc-web-gui    # used to drive graphical frontend  # https://rclone.org/gui/
-
- > To copy the config from one machine to another:
  To find this file, run `rclone config file` which will tell you where it is.
  /home/briandanks/.config/rclone/rclone.conf
-
	- https://rclone.org/commands/rclone_copy/     # to copy files accross but not copy identical src/dest
	- ```bash
	  ### Note: --dry-run or the --interactive/-i flag to test without copying anything
	  
	  rclone copy source:sourcepath dest:destpath
	  
	  #For example, if you have many files in /path/to/src but only a few of them change every day, you can copy all the files which have changed recently very efficiently like this:
	  rclone copy --max-age 24h --no-traverse /path/to/src remote:
	  
	  ```
-
- https://rclone.org/commands/rclone_dedupe/  # many options!
- ==e.g== `rclone dedupe --by-hash --dry-run -P  /home/briandanks/zxcBackup`
-
- `rclone authorize "drive" "eyJzY29wZSI6ImRyaXZlIn0"`
  ==e.g.== `rclone copy -P gdrive_baking: .`
- {{video https://youtu.be/YDF1nBaAptw}}
-
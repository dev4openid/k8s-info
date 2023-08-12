- find config file at .config/rclone/rclone.conf
- pwd: 1Catinahat
- rclone  https://rclone.org
       https://wiki.linuxquestions.org/wiki/Rsync_with_Google_Drive
- rclone config
  rclone rcd --rc-web-gui    # used to drive graphical frontend  # https://rclone.org/gui/
-
- > Can I copy the config from one machine to another 
  To find this file, run `rclone config file` which will tell you where it is.
- https://rclone.org/commands/rclone_dedupe/  # many options!
-
- `rclone authorize "drive" "eyJzY29wZSI6ImRyaXZlIn0"`
  ==e.g.== `rclone copy -P gdrive_baking: .`
- {{video https://youtu.be/YDF1nBaAptw}}
-
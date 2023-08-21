- [Images prevent AI Recognition](https://github.com/Shawn-Shan/fawkes)
- Connect Ubuntu and iPhone
-
- ==Ref:==
- https://www.maketecheasier.com/easily-mount-your-iphone-as-an-external-drive-in-ubuntu/
- http://sandlab.cs.uchicago.edu/fawkes/#code
-
- ```bash
  sudo apt install libimobiledevice6 libimobiledevice-utils usbmuxd
  sudo apt install ifuse
  
  mkdir ~/iphone
  
  # engage iphone with lightning cable then
  idevicepair pair
  usbmuxd -f -v
  
  # better still just use 
  ifuse ~/iphone
  
  # to remove/unmount device
  # ifuse -u /iphone
  ```
-
-
- ##Clean up EXIF info on image
- ```bash
  tldr exiftool
  # then use to remove all data
  exiftool -All= ./IMG_0664.jpg
  # then check data all gone
  exiftool  ./IMG_0664.jpg
  
  ```
-
- Get code from github for Linux
- >./protection -d ./images -m high --format jpg
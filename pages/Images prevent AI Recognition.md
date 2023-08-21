- [Images prevent AI Recognition](https://github.com/Shawn-Shan/fawkes)
- Connect Ubuntu and iPhone
-
- Ref:
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
- tl
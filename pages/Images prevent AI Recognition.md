- [Images prevent AI Recognition](https://github.com/Shawn-Shan/fawkes)
- Conect Ubuntu and iPhone
- ```bash
  sudo apt install libimobiledevice6 libimobiledevice-utils
  sudo apt install ifuse
  
  mkdir ~/iphone
  
  # engage iphone with lightning cable
  idevicepair pair
  usbmuxd -f -v
  
  ifuse ~/iphone
  ```
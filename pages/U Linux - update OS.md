- ```bash
  !/bin/bash
  printf "\n________apt update\n"
  sudo apt-get update -y
  printf "\n________apt upgrade\n"
  sudo apt-get upgrade -y
  printf "\n________apt-get full-upgrade\n"
  sudo apt-get full-upgrade -y
  printf "\n________apt full-upgrade\n"
  printf "\n________apt autoremove\n"
  sudo apt-get autoremove --purge
  printf "\n________apt purge\n"
  sudo apt-get purge
  printf "\n________apt clean\n"
  sudo apt-get clean
  printf "\n________apt autoclean\n"
  sudo apt-get autoclean
   
  # the below is deb-get
  printf "\n________deb-get updates"
  sudo deb-get update
  sudo deb-get upgrade
   
  # the below is the snap refesh to latest versions
  printf "\n________snap refresh\n"
  sudo snap refresh
   
  # the below is the brew update/upgrade
  printf "\n________bubu!!!!!!!!!!!!!!!! problem here\n"
  brew update
  brew upgrade
  brew cleanup
   
  # Remove old_kernels
  printf "\n________remove old kernels\n"
  sudo ~/remove_old_kernels.sh exec
   
  # Upgrade Pihole
  printf "\n________upgrade Pihole\n"
  pihole -up
  
  ```
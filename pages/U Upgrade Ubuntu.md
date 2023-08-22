- https://sypalo.com/how-to-upgrade-ubuntu
-
- # Preparation
	- ```bash
	  # Update packages list
	  sudo apt-get update
	  # Upgrade packages
	  sudo apt-get upgrade
	  #Install update-manager-core package
	  
	  ```
	-
- ## Update Ubuntu to 23.04
	- ```bash
	  # Upgrade distro
	  sudo apt-get dist-upgrade
	  # Update Ubuntu to the latest LTS release
	  # Run the following command until you get your Ubuntu to version 22.04:
	  sudo do-release-upgrade
	  
	  ```
	-
- ## Change default branch from lts to normal
	- Once you update your Ubuntu to 22.04, the latest LTS version, you need to tell the update manager to get the newest short-term supported Ubuntu 23.04. If you want to test new features and are an experienced Linux user you can upgrade to the currently developed 23.04. But remember to back up all your important files in advance, especially if you are going to upgrade your live pc, laptop, or server. But better to test the upgrade on a VM first. The main rule - the fewer versions you are skipping the soother the upgrade process will be, so if you would like to upgrade directly from say 20.04 to 23.04 the process most likely will fail or you will get a bunch of errors and need to fix broken packages and re-run the upgrade again. So I told you - better be safe than sorry, and now let`s move on.
	- ```bash
	  sudo sed -i 's/lts/normal/g' /etc/update-manager/release-upgrades
	  
	  ```
	-
- ## Change default distro from your current
	- 20.04 - focal
	- 20.10 - groovy
	- 21.04 - hirsute
	- 21.10 - impish
	- 22.04 - jammy
	- 22.10 - kinetic
	- 23.04 - lunar
	- 23.10 - mantic (development branch)
	- in the example below, we are upgrading from Ubuntu 22.04 (jammy) to 23.04 (lunar)
	- ```bash
	  sudo sed -i `s/jammy/lunar/g` /etc/apt/sources.list
	  # Update packages list
	  sudo apt-get update
	  sudo apt-get upgrade
	  # Run full upgrade
	  sudo apt-get dist-upgrade
	  
	  # If any error re-run
	  
	  
	  
	  
	  ```
	-
	- If any error re-run
		- >sudo apt-get update
		- >sudo apt-get dist-upgrade
	- Run cleanup
		- >sudo apt-get autoremove
		- sudo apt-get clean
	- Reboot the system
		- sudo reboot
		- Update packages list
			- sudo apt-get update
		- Upgrade packages
			- sudo apt-get upgrade
		- Run full upgrade
			- sudo apt-get dist-upgrade
		- If any error re-run
			- sudo apt-get update
			- sudo apt-get dist-upgrade
		- Run cleanup
			- sudo apt-get autoremove
			- sudo apt-get clean
		- Reboot the system
			- sudo reboot
			-
- ## Upgrade Ubuntu kernel version
	- 1.  Change current directory to /tmp
		- cd /tmp
	- 2.  Download latest stable kernel
		- ```
		      wget -c [https://kernel.ubuntu.com/~kernel-ppa/mainline/v6.4.11/amd64/linux-headers-6.4.11-060411_6.4.11-060411.202308161732_all.deb](https://kernel.ubuntu.com/~kernel-ppa/mainline/v6.4.11/amd64/linux-headers-6.4.11-060411_6.4.11-060411.202308161732_all.deb)  
		      wget -c [https://kernel.ubuntu.com/~kernel-ppa/mainline/v6.4.11/amd64/linux-headers-6.4.11-060411-generic_6.4.11-060411.202308161732_amd64.deb](https://kernel.ubuntu.com/~kernel-ppa/mainline/v6.4.11/amd64/linux-headers-6.4.11-060411-generic_6.4.11-060411.202308161732_amd64.deb)  
		      wget -c [https://kernel.ubuntu.com/~kernel-ppa/mainline/v6.4.11/amd64/linux-image-unsigned-6.4.11-060411-generic_6.4.11-060411.202308161732_amd64.deb](https://kernel.ubuntu.com/~kernel-ppa/mainline/v6.4.11/amd64/linux-image-unsigned-6.4.11-060411-generic_6.4.11-060411.202308161732_amd64.deb)  
		      wget -c [https://kernel.ubuntu.com/~kernel-ppa/mainline/v6.4.11/amd64/linux-modules-6.4.11-060411-generic_6.4.11-060411.202308161732_amd64.deb](https://kernel.ubuntu.com/~kernel-ppa/mainline/v6.4.11/amd64/linux-modules-6.4.11-060411-generic_6.4.11-060411.202308161732_amd64.deb)
		    ```
	- 3.  Install latest stable kernel
		- >sudo dpkg -i *.deb
	- 4.  Reboot system after latest stable kernel upgrade
		- >sudo reboot
	- 5.  Change current directory to /tmp
		- >cd /tmp
	- Download latest mainline kernel (optionally)
		- If you experience some issues with the latest stable kernel or want to test the newest release candidate you might give the latest kernel release candidate a try. But be cautious, it is still in development, and while fixing some bugs, new ones might appear. There are two ways to install latest mainline kernel:
			- ```bash
			      sudo add-apt-repository ppa:cappelikan/ppa -y
			      sudo apt-get update
			      sudo apt-get update
			      sudo apt install mainline -y
			  ```
		- or:
		- ```bash
		  ```
		-
		-
		- wget -c [https://kernel.ubuntu.com/~kernel-ppa/mainline/v6.5-rc7/amd64/linux-headers-6.5.0-060500rc7_6.5.0-060500rc7.202308201631_all.deb](https://kernel.ubuntu.com/~kernel-ppa/mainline/v6.5-rc7/amd64/linux-headers-6.5.0-060500rc7_6.5.0-060500rc7.202308201631_all.deb)
		- wget -c [https://kernel.ubuntu.com/~kernel-ppa/mainline/v6.5-rc7/amd64/linux-headers-6.5.0-060500rc7-generic_6.5.0-060500rc7.202308201631_amd64.deb](https://kernel.ubuntu.com/~kernel-ppa/mainline/v6.5-rc7/amd64/linux-headers-6.5.0-060500rc7-generic_6.5.0-060500rc7.202308201631_amd64.deb)
		- wget -c [https://kernel.ubuntu.com/~kernel-ppa/mainline/v6.5-rc7/amd64/linux-image-unsigned-6.5.0-060500rc7-generic_6.5.0-060500rc7.202308201631_amd64.deb](https://kernel.ubuntu.com/~kernel-ppa/mainline/v6.5-rc7/amd64/linux-image-unsigned-6.5.0-060500rc7-generic_6.5.0-060500rc7.202308201631_amd64.deb)
		- wget -c [https://kernel.ubuntu.com/~kernel-ppa/mainline/v6.5-rc7/amd64/linux-modules-6.5.0-060500rc7-generic_6.5.0-060500rc7.202308201631_amd64.deb](https://kernel.ubuntu.com/~kernel-ppa/mainline/v6.5-rc7/amd64/linux-modules-6.5.0-060500rc7-generic_6.5.0-060500rc7.202308201631_amd64.deb)
- ## Finishing up
	- Update packages list
		- >sudo apt-get update
	- Upgrade packages
		- >sudo apt-get upgrade
	- Reboot the system if needed
		- >sudo reboot
	- Check the OS distro
		- >lsb_release -a
	- Check kernel version
		- >uname -r
- # Docker networks  (Total 7 types)
- [[KK Docker]]
- These are: bridge / hosts  / mac-vlan
  Bridge: is the connection via the default bridge ---> so better to define your own network (User-defined bridge)
	- ```cmake
	  sudo docker network create mybridge
	  4f6354fdf208b37ee919fcb184b8e040e2ba974d445e9f744a9cb2609bc049b2
	  docker network ls       # --->
	  NETWORK ID     NAME       DRIVER    SCOPE
	  9ce45ca2c596  bridge       bridge     local
	  adb4bbc8b63a host           host        local
	  4f6354fdf208    mybridge  bridge    local
	  8cfb809909bd  none          null         local
	  
	  # Note: all containers will belong to default host (IP range of 172.17.0.2) unless defined against new network
	  e.g. 
	  sudo docker run -itd --rm --network mybridge --name bbox busybox
	  	# ---> results in 172.18.0.1 for bbox - which is an isolated network from the default
	      
	  	# Note: if bbox was a webserver then the netwotk post must be exposed
	  e.g.
	  sudo docker run -itd --rm -p 8080:80 --name mynginx nginx
	  5aeb64da99f7a853436ea1cea413f34e059bc81e71111e6c18e292727d090fc7
	     # ---> In browser 192.168.1.106:8080 results in nginx webser defaults
	  
	  ```
- Host: These are defined against your own network and leverage your current IP address (your PC)
	- ```cmake
	  sudo docker run -itd --rm --network host  --name mynginx nginx
	  c92b61ff73ecf908753dbebb4870cbd284f133eec7aaae85a0d6e064971039b2
	  
	  # go to browser and connect to IP Address of nginx and is will be like any other app - it is still a container on host
	  # e.g. wireguard can be run on host without the virtual IP address as another app
	  ```
- mac-vlan:
	- ```cmake
	  sudo docker network create -d macvlan --subnet 192.168.1.1/24 --gateway 192.168.1.1 -o parent=enp1s0f0 newmynetwork #name of network
	      # get this - enp1s0f0 - from: ip address show AND look the host ref
	  c92b61ff73ecf908753dbebb4870cbd284f133eec7aaae85a0d6e064971039b2
	  
	  # Note: It can work BUT there is no DNS and NIC setting must be in promiscious mode. In addition the host may have to be rebooted
	  # All containers have to be maually configured with IP addresses (hopefully no conflicts)
	  
	  # 2 modes - 1st as bridge mode (with the above issues) and 2nd being the second variant
	  sudo docker network create -d macvlan --subnet 192.168.20.1/24 --gateway 192.168.20.1 -o parent=enp1s0f0.20 macvlan20
	  7f78d537ccb67f446986d64bd03f7a2593e91b6ce8cd0cf9db5a30bfa8a75f89
	  ```
- ipvlan L2 (default) and L3
	- ```cmake
	  sudo docker network create -d ipvlan --subnet 192.168.0.1/24 --gateway 192.168.0.1 -o parent=enp1s0f0 ipvlanL2       
	  6b29af225c4016ce41346095e6739077e20e43c07ef509c521f6a95eba54f508
	  # alternative for multiple networks:
	  sudo docker network create -d ipvlan --subnet 192.168.94.0/24 --subnet 192.168.95.0/24 -o ipvlan=l3 -o parent=enp1s0f0.20 ipvlanL3 
	  ffd99c650b02f0115a4849ddfe3ca7bbb9ada5671a71afde08ac6e50d430a086
	  
	  sudo docker network ls
	  NETWORK ID     NAME       DRIVER    SCOPE
	  9ce45ca2c596   bridge     bridge    local
	  adb4bbc8b63a   host       host      local
	  6b29af225c40   ipvlanL2   ipvlan    local
	  8cfb809909bd   none       null      local
	  
	  sudo docker run -itd --rm --network ipvlanL2  --ip 192.168.0.30 --name bbox busybox
	  7d5c8952a447d12537a3b889980496c9330641b35547a3b135a0d52d33ec84bf
	    #	Note the IP has to be specified maually
	  sudo docker exec -it bbox sh
	  / # ip address show
	  1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue qlen 1000
	      link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
	      inet 127.0.0.1/8 scope host lo
	         valid_lft forever preferred_lft forever
	  21: eth0@if2: <BROADCAST,MULTICAST,UP,LOWER_UP,M-DOWN> mtu 1500 qdisc noqueue 
	      link/ether 68:5b:35:b3:27:f9 brd ff:ff:ff:ff:ff:ff
	      inet 192.168.0.30/24 brd 192.168.0.255 scope global eth0
	         valid_lft forever preferred_lft forever
	     # one can ping all containers in the range e.g. 192.168.0.40
	  ```
- ipvlan L3
	- ```cmake
	  sudo docker network create -d ipvlan --subnet 192.168.94.0/24 -o ipvlan=l3 -o parent=enp1s0f0.20 ipvlanL3
	  acfbde0f7fe3f30154179deff679c6468b5e15ef61b69643de2572dc7cc08539
	  
	  sudo docker network ls
	  NETWORK ID     NAME       DRIVER    SCOPE
	  9ce45ca2c596   bridge     bridge    local
	  adb4bbc8b63a   host       host      local
	  6b29af225c40   ipvlanL2   ipvlan    local
	  8cfb809909bd   none       null      local
	  
	  sudo docker run -itd --rm --network ipvlanL3  --ip 192.168.94.7 --name bbox busybox 
	  8105bf0d82305532fa87bc9460c2b31a929ee65365b421fc22143f61fb4220d3
	  
	  sudo docker run -itd --rm --network ipvlanL3  --ip 192.168.94.8 --name b-bbox busybox 
	  85126ace7e3db1ae71cf33fff1306ba110f28d9a13374c472ee229e66ef1e8c8      # same network scope
	  
	  sudo docker run -itd --rm --network ipvlanL3  --ip 192.168.95.7 --name obbox busybox 
	  d292182259a1549b057a86f74bf5a974df324738d5a6f96f14033950a63e7fe1
	  
	  sudo docker run -itd --rm --network ipvlanL3  --ip 192.168.95.8 --name ob-bbox busybox 
	  494b5894bb4edff545eb200f778d7d84584afd851f09fcbecbe833fe748939d3
	  
	  sudo docker inspect ipvlanL3
	  	# ---> notice all IPs are present
	      
	  # Note: all IPs in ipvlanL3 can ping each other
	  #       also, if above IPs are defined in router as static IPs then any of IP can connect externally and local network can ping the assigned IPs 
	  ```
- Overlay
	- This is to overlay multiple IP clusters - removes complexity - used by Docker swarm or Kubernetes
- the None
	- ```cmake
	  sudo docker run -itd --rm --network none --name bbox busybox
	  4d8c26372f13be144a83a8264b2782b49802512adaf09db63a4d450e7ffa3f7b
	  
	  sudo docker exec -it bbox sh
	  / # ip address show
	  1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue qlen 1000
	      link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
	      inet 127.0.0.1/8 scope host lo
	         valid_lft forever preferred_lft forever
	  # there is no network at all
	  ```
-
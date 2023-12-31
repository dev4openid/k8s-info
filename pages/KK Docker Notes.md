- # Docker notes
- Remote docker container:
- ```cmake
  e.g.
  	docker -H=remote-docker-engine:2375	# remote-docker-engine is IP number
      docker -H=10.123.2.1:2375 run nginx
  ```
- cgroups
	- docker run --cpus=.5 ubuntu           # cannot have more than 50% of cpus
	- docker run --memory=.100m ubuntu      # cannot have more than 100 MB of memory
- File Systems
	- docker stores all files in:
	- /var/lib/docker
		- aufs
		- containers
		- image
		- volumes
-
- docker volume create data-volume --->
	- >e.g. Default: (Volume Mount)
	  /var/lib/docker/volumes/data-volume
	  so run docker: docker run -v data-volume:/var/lib/mydql mysql
	- >e.g Another somewhere else: (/data/mysql) (Bind Mount)
	  docker run - v /data/mysql:var/lib/mysql mysql
	  read as from where the volume exists (/data/mysql), mount it to mysql expected storage being var/lib/mysql mysql
	- >*==Notes:==* docker run --mount type=bind,source=/data/mysql,target=var/lin/sql mysql  (Modern Method)
- Storage drivers:
	- aufs
	- zfs
	- btrfs
	- Device Mapper
	- Overlay
	- Overlay2
- Networks
	- docker network create --driver bridge --subnet 182.18.0.0/16 custom-isolated-network
		- ---> e.g. docker run --network=none --name=alpine-2 alpine
		- ---> docker network create --driver bridge --subnet 182.18.0.1/24 wp-mysql-network
		- ---> docker network create --driver bridge --subnet 182.18.0.1/24 --gateway 182.18.0.1 wp-mysql-network
		- ---> docker network rm wp-mysql-network    # to rmove networks
	- internal DNS is at 127.0.0.11
- Registry
	-
		- docker tag postgres localhost:5000/postgres                 # note the image pulled/created must be TAGGED
		- ```cmake
		  # create 'local' registry
		  docker run -d -p 5000:5000 --restart always --name registry -v $(pwd)/docker-registry:/var/lib/registry registry:latest 
		  
		  ---> OR --name cerebra1.com --- note the restart always aspect include  
		      ---> - not necessary AND note the pwd
		  
		  	---> local to environment   OR cerebra1.com/5000/registry
		  
		  # To enable local/remote host NON-HTTPS repository
		  # sudo vi /etc/docker/daemon.json
		  {
		      "insecure-registries": [
		          "192.168.1.106:5000"
		      ],
		      "experimental": false
		  }
		  
		  sudo systemctl stop docker
		  sudo systemctl start docker
		  sudo systemctl status docker
		  
		  docker tag  nginx 192.168.1.106:5000/nginx	# note the image pulled/created must be TAGGED
		  docker push 192.168.1.106:5000/nginx	    # to push postgres into the local registry
		  
		  curl -X GET http://localhost:5000/v2/_catalog 	# no preferred route !localhost
		  curl -X GET http://192.168.1.106:5000/v2/_catalog
		  	---> {"repositories":["nginx"]}			# this is what it should reflect
		  # to return the image:
		  docker pull http://192.168.56.100:5000/nginx   # local is 192.168.56.100
		  
		  docker images --digests
		  
		  
		  ```
		- docker pull 192.168.56.100:5000/postgres   # local is 192.168.56.100
-
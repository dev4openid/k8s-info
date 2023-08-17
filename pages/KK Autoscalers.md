- # Autoscalers
  title:: KK Autoscalers
- HPA (Horizonatal Pod Autoscaler  - Horiz.Scaling)
- VPA (Vertical Pod Autoscaler - Scale UP)
- CA (Cluster Autoscaler - add new/reduce # of Nodes)
### HPA
	- ![How HPA calculates number of Pods](/home/briandanks/Pictures/Screenshots/Screenshot from 2023-07-04 20-12-06.png)
	- How HPA calculates number of Pods
### VPA
	- ![Vertical Pod Autoscaler](/home/briandanks/Pictures/Screenshots/Screenshot from 2023-07-04 20-24-17.png)
	- Vertical Pod Autoscaler
	- To install
		- ```cmake
		  git clone https://github.com/kubernetes/autoscaler.git
		  cd autoscaler
		  ./vertical-pod-autoscaler/hack/vpa-up.sh   # note therer are other functions in vpa-down.sh / etc.
		  cd ..	# in this example
		  kubectl apply -f vpa.yaml # vpa in this example
		  ```
### CA
- ![Cluster Autoscaler](/home/briandanks/Pictures/Screenshots/Screenshot from 2023-07-04 20-40-41.png)
- Cluster Autoscaler
-
- # Taints and Tolerations
  title:: KK Taints and Tolerations
- Taint is defined in the Node # gives of the smell 🙄
- ```yaml
  metadata:
    labels:
  	# key: value:taint-effect
      app: blue:NoSchedule      	# alternatives are PreferNoSchedule, NoExecute
  ```
- cli version: `kubectl taint node node01 app=blue:NoSchedule` AND to remove the taint `kubrctl taint node controlplane node-role.kubernetes.io/master:NoScheduler-`       # It is the appending '-' that removes the taint from node
- Tolerance is defined in the Pod  # defines if it is tolerant of the smell 😁
- ```yaml
  apiVersion: v1
  kind: Pod
  metadata:
    name: nginx
  spec:
    containers:
    - name: nginx
      image: nginx:1.20.2
      ports:
      - containerPort: 80
    tolerations:	# KOVE			# this drives the aversion (or not) to assoc with Node
    - key: "app"
    	operator: "Equal"
      value: "blue"
      effect: "NoSchedule"	
      		# alternatives are	"PreferNoSchedule", 
      		#					"NoExecute" (evict OLD Pods that cannot tolerate the taint)
      	# NOTE: the above MUST USE ""
  
  ```
- cli version: ?????
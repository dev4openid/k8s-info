- 🔥 Main Kubectl Commands - K8s CLI 🔥
  ► Get status of different components
  ► create a pod/deployment
  ► layers of abstraction
  ► change the pod/deployment
  ► debugging pods
  ► delete pod/deployment
  ► CRUD by applying configuration file
- 🔗 Links:
- Git repo link of all the commands: [https://bit.ly/3oZzuHY](https://bit.ly/3oZzuHY)
- Git repo link: [https://bit.ly/3jY6lJp](https://bit.ly/3jY6lJp)
-
## Main Kubectl Commands - K8s CLI  (00:44:52)
- ### Minikube
- minikube start / stop / delete / status
  minikube dashboard (overview of env and can do more! - more later)
- example `minikube start --nodes 2 -p local-cluster  --disk-size='5gb' --driver=docker
- ` (*optional is ---> namespace=learn*) --> careful here on what thew driver facilitates irt services!! e.g. quemu or quemu2
- the input allow options such as namespave, disk alloc, driver to be use, etc.   `minikube start --help
- `
- *==Tips:==*
- create additional worker nodes e.g. `minikube node add --worker -p local-cluster
- ` ---> local-cluster is a node name
- `minikube  addons enable metrics-server -p local-cluster
- ` to generate metrics for dashboard
- `minikube dashboard --url -p local-cluster
- `
- `minikube addons enable ingress-p local-cluster
- ` ---> allow ingress point into minikube
- *==Note:==* the `-p local-cluster
- ` to apply to the correct cluster!!
- `minikube status
- `
- result are similar to:
- minikube
- type: Control Plane
  host: R
- unning
- kubelet: Running
  apiserver: Running
  kubeconfig: Configured
-
- ### kubectl
- ![kubectl command structure](/home/briandanks/Pictures/Screenshots/Screenshot from 2023-06-23 09-12-10.png){:height 338, :width 668}
- `kubectl version`
- create deployment   (abstraction over pods)
	- `kubectl create deployment nginx-depl --image=nginx` -- image can be versioned to nginx:1.16 as e.g.
	- with the result of a pod instance
	- Note: kubctl create deployment .........results in:
		- blueprint for creating pods
		- most basic configuration for deployment (name and image to be used)
		- rest are defaults (unless specified)
- `kubectl get deployment`
	- NAME         READY   UP-TO-DATE   AVAILABLE   AGE
	  nginx-depl   1/1          1                     1                    19s
- `kubectl get pod`
	- NAME                                           READY   STATUS    RESTARTS   AGE
	  nginx-depl-56cb8b6d7-pwlmz   1/1         Running    0                  34m
- `kubectl exec -it nginx-depl-56cb8b6d7-pwlmz -- bin/bash`
	- root@nginx-depl-56cb8b6d7-pwlmz:/#   ---> this allows root control of pod itself
- `kubectl edit deployment`
	- ```yaml
	  # Please edit the object below. Lines beginning with a '#' will be ignored,
	   # and an empty file will abort the edit. If an error occurs while saving this file will be
	   # reopened with the relevant failures.
	   #
	   apiVersion: apps/v1
	   kind: Deployment
	   metadata:
	     annotations:
	       deployment.kubernetes.io/revision: "1"
	     creationTimestamp: "2023-06-15T16:44:19Z"
	     generation: 1
	     labels:
	       app: nginx-depl
	     name: nginx-depl
	     namespace: default
	     resourceVersion: "579"
	     uid: 6275d61d-07e6-4f0f-85ed-2501e40ce828
	   spec...
	  ```
- ==Tip:==
	- To generate a core yaml file for an image type do as per e.g. below:
	- `run nginx --image=nginx --dry-run=client -o YAML > zxc.yaml` # there is also -dry-run=server
- Note: the kubectl deployment can be manipulated by:
	- `kubectl create deployment ...`
	- `kubectl edit deployment ...`
	- `kubectl delete deployment ...`
	-
- `kubectl get replicaset`
	- NAME                               DESIRED   CURRENT   READY   AGE
	  nginx-depl-56cb8b6d7   1                1                  1             53m
-
- Note: By editing the deployment replicasets and/or other configs realising in the outcome desired
- ***Note:***
	- Deployment manages a ..
	  Replicaset manages a ..
	  Pod is an abstraction of ..
	  Container
- `kubectl apply -f config-file.yaml`
	- *deployment.apps/nginx-deployment created*
	  *deployment.apps/nginx-deployment configured*
	- Note the difference above - 1 to create and 1 to change the config
-
- Summary:  (01:01:43)
	- Status of different K8s components:
		- kubectl get nodes | service | replicaset | deployment
	- *==Debugging pods:==*
		- log to console ---> `kubectl logs nginx-deployment-68d9b6c666-ksx2w` [pod name]
		- `kubectl describe pod nginx-deployment-68d9b6c666-ksx2w`
		- `kubectl exec -it nginx-deployment-68d9b6c666-ksx2w -- bin/bash` ---> this is to get into pod instance
		- `kubectl exec -it nginx-deployment-68d9b6c666-ksx2w -c nginx-container -- bin/bash`---> this is to access the nginx in the pod instance
		- `kubectl port=forward service/nginx-service 8083:8080` ---> means you now can access the service  via the  browser: localhost:8083 - this will show nginx
- *==TIP:==* To delete a Service OR/AND Pod OR/AND Deployment use:
	- `kubectl delete service nginx-service`
	- `kubectl delete pod nginx-service`
	- `kubectl delete deployment  nginx2-depl`
-
- ### Managing Deployments
	- *==TIP:==*
		- `kubectl delete all --all` means all resources in namespace are deleted
		- Always leverage the apply - f filename.yaml rather than cli
	- ### History and reversion
	- `kubectl rollout history deployment/mongodb-deployment`---> provides the history of the deployment
	- `~kubectl rollout undo deployment/mongodb-deployment --to-revision=2`---> revert to a specific version
-
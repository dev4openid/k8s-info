- Ingress (02:01:52)
- ## External Service vs. Ingress
  > Place Ingress in front of "external service" (which becomes internal); this way anyone with the url can access the application (via the external service) via the Ingress (which masks the k8s internals)
- ![Ingress Concepts](/home/briandanks/Pictures/Screenshots/Screenshot from 2023-06-23 17-32-50.png){:height 382, :width 708}
- Ingress Concepts
- Ingres yaml:
- ![Ingres mapping to "external service"](/home/briandanks/Pictures/Screenshots/Screenshot from 2023-06-21 18-38-45.png){:height 298, :width 756}
- Ingres mapping to "external service" (now converted to an internal service)
- Note the url is http (not https) and the e.g. is browser my-app.com points to the host (in Ingress) ---> unless there is a TLS defined and included as a secret
- ## Converting external service to internal service (to support Ingress)
- In the Service: 
  the nodePort is removed AND
  the spec - type is not Loadbalancer but ClusterIP  (NB: the internal service has "built-in loadbalancer")
- Ingress host must be a valid domain name!
- >*==Note:==* Ingress sets up ==mapping== to access internal service etc.
- Require an Ingress Controller Pod (which is mapped to Ingress)
	- which evaluates and processes Ingress rules - entrypoint to K8s cluster and is part of the cluster
- ![Ingress Controller to Ingress](/home/briandanks/Pictures/Screenshots/Screenshot from 2023-06-21 18-51-47.png){:height 379, :width 552}
- Ingress Controller to Ingress
- There are many Ingress Controllers  - e.g.
	- [NGINX Ingress Controller for Kubernetes](https://www.nginx.com/products/nginx-ingress-controller/),
	- [Traefik Kubernetes Ingress provider](https://doc.traefik.io/traefik/providers/kubernetes-ingress/))  refer to https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/
- If using minikube invoke `minikube addons enable ingress -p local-cluster` resulting:
	- ```cmake
	  minikube addons enable ingress -p local-cluster
	  💡  ingress is an addon maintained by Kubernetes. For any concerns contact minikube on GitHub.
	  You can view the list of minikube maintainers at: https://github.com/kubernetes/minikube/blob/master/OWNERS
	      ▪ Using image registry.k8s.io/ingress-nginx/controller:v1.7.0
	      ▪ Using image registry.k8s.io/ingress-nginx/kube-webhook-certgen:v20230312-helm-chart-4.5.2-28-g66a760794
	      ▪ Using image registry.k8s.io/ingress-nginx/kube-webhook-certgen:v20230312-helm-chart-4.5.2-28-g66a760794
	  🔎  Verifying ingress addon...
	  🌟  The 'ingress' addon is enabled
	  ```
	- which is the implementation of the [NGINX Ingress Controller for Kubernetes](https://www.nginx.com/products/nginx-ingress-controller/) in minikube
	- from `kubectl get pod -n kube-system` check results in
	- ``` cmake
	  kubectl get pod -n kube-system  
	  NAME                               READY   STATUS    RESTARTS   AGE
	  coredns-787d4945fb-f6nll           1/1     Running   0          8h
	  etcd-minikube                      1/1     Running   0          8h
	  kube-apiserver-minikube            1/1     Running   0          8h
	  kube-controller-manager-minikube   1/1     Running   0          8h
	  kube-proxy-8knbz                   1/1     Running   0          8h  ---> this is the nginx-ingress-controller
	  kube-scheduler-minikube            1/1     Running   0          8h
	  storage-provisioner                1/1     Running   0          8h
	  ```
	-
- `minikube ip -p local-cluster` results in 192.168.49.2 which is the entry point to the cluster
- >*==Note:==*
  > In ingress video at 11:23 look at paths and what they mean - Exact or Prefix
  > On the cloud, map the CNAME to the loadbalancer
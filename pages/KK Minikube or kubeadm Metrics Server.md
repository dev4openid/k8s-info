- # Metrics Server
- getting metrics-server
- minikube `minikube addons enable metrics-server`
- adm or other `git clone https://github.com/kubernetes-sigs/metrics-server.git` then `kubectl create -f deploy/1.8+/` OR
- ```
  kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
  ```
- [Metrics-server](https://github.com/kubernetes-sigs/metrics-server)
- Exec: `kubectl top node` OR `kubectl top pod`
-
-
-
-
-
-
- SCHEDULING ISSUE
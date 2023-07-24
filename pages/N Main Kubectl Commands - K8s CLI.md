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
-
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
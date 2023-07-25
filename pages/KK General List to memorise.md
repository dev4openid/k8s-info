- # General List to memorise
  title:: KK General List to memorise
- volume
- configmap
- secret
- pod
- service
- ingress
- deployment
- sts
### Node Components
- > Container runtime  ---> The container runtime is the software that is responsible for running containers.
  > kubelet            ---> An agent that runs on each node in the cluster. It makes sure that containers are running in a Pod.
  > kubeproxy          ---> kube-proxy is a network proxy that runs on each node in your cluster, implementing part of the Kubernetes Service concept.
### Control Plane Components
- > kube-apiserver           --->The API server is a component of the Kubernetes control plane that exposes the Kubernetes API. The API server is the front end for the Kubernetes control plane
  etcd                     --> Consistent and highly-available key value store used as Kubernetes' backing store for all cluster data
  kube-scheduler           ---> Control plane component that watches for newly created Pods with no assigned node, and selects a node for them to run on
  kube-controller-manager ---> Control plane component that runs controller processes
  cloud-controller-manager ---> A Kubernetes control plane component that embeds cloud-specific control logic
-
- | Component| Description|
- | kube-apiserver | The API server is a component of the Kubernetes control plane that exposes the Kubernetes API. The API server is the front end for the Kubernetes control plane |
- |kube-apiserver |
- |||
- |--|--|
- | Control plane component that runs controller processes | 
  | etcd | Consistent and highly-available key value store used as Kubernetes' backing store for all cluster data |
  | kube-controller-manager | Control plane component that runs controller processes |
  | cloud-controller-manager | A Kubernetes control plane component that embeds cloud-specific control logic |
- |Component|Description|
  |--|--|
  |kube-apiserver|The API server is a component of the Kubernetes control plane that exposes the Kubernetes API. The API server is the front end for the Kubernetes control plane|
  |kube-scheduler |Control plane component that watches for newly created Pods with no assigned node, and selects a node for them to run on |
  |kube-controller-manager |Control plane component that runs controller processes |
  |cloud-controller-manager |A Kubernetes control plane component that embeds cloud-specific control logic |
- |etcd |Consistent and highly-available key value store used as Kubernetes' backing store for all cluster data |
-
### yaml file format
- >apiVersion
  Kind
  Metadata
  Spec
- kubectl port-forward svc/mongodb-service 32000/27017  # an e.g. ()if you want to check areas with nodePort defined)
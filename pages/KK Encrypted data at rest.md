- Encrypted data at rest
-
- >Use etcdctl  (install in environments from https://etcd.io/docs/v3.5/install/ which leads to https://github.com/etcd-io/etcd/releases/)
  Ensure thaat the ca.crt server.crt server.key are incorporated into etcd (which they should already be therein on startup)
  Refer to https://kubernetes.io/docs/tasks/administer-cluster/certificates/ point 3
- From `k edit pod etcd-minikube -n kube-system` extract the certs and keys
-
- >ETCDCTL_API=3 etcdctl \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
   --cert=/etc/kubernetes/pki/etcd/server.crt \
   --key=/etc/kubernets/pki/etcd/server.key \
   get /registry/sectrets/default/secret1 | hexdump
-
-
- For ssh into minikube `ssh minikube`
  cd /var/lib/minikube/certs
  ls -la
-
- ```cmake
  ETCDCTL_API=3 etcdctl \
  --cacert=var/lib/minikube/pki/etcd/ca.crt \
   --cert=/var/lib/minikube/pki/etcd/server.crt \
   --key=var/lib/minikube/pki/etcd/server.key \
   get /registry/sectrets/default/secret1 | hexdump
  ```
- /var/lib/minikube/certs/etcd/ca.crt
- /var/lib/minikube/certs/etcd/server.crt
- /var/lib/minikube/certs/etcd/server.key
-
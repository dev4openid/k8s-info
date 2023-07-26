- Encrypted data at rest
-
- >Use etcdctl  (install in environments from https://etcd.io/docs/v3.5/install/ which leads to https://github.com/etcd-io/etcd/releases/)
  Ensure thaat the ca.crt server.crt server.key are incorporated into etcd (which they should already be therein on startup)
  Refer to https://kubernetes.io/docs/tasks/administer-cluster/certificates/ point 3
-
-
- ```cmake
  ETCDCTL_API=3 etcctl \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
   --cert=/etc/kubernetes/pki/etcd/server.crt \
   --key=/etc/kubernets/pki/etcd/server.key \
   get /registry/sectrets/default/secret1 | hexdump
  ```
- /var/lib/minikube/certs/etcd/ca.crt
- cert-file=/var/lib/minikube/certs/etcd/server.crt
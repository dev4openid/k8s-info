- # RBAC
- ## Introduction:
- ![Overall view of k8s infrastructure](/home/briandanks/Pictures/Screenshots/Screenshot from 2023-07-05 10-15-58.png){:height 370, :width 650}
- Overall view of k8s infrastructure
- Check `vi ~/.kube/config`
- ## To add a new user:
- ```cmake
  #create a user key: 
  openssl genrsa -out briand.key
  # --> briand.key
  
  # create a user csr cert
  openssl req -new -key briand.key -out briand.csr -subj "/CN=briand/O=dev/O=example.org"
  # ---> briand.csr
  
  # get signed by minikube the crt (token)
  openssl x509 -req -CA ~/.minikube/ca.crt -CAkey ~/.minikube/ca.key -CAcreateserial -days 750 -in briand.csr -out briand.crt
  Certificate request self-signature ok
  subject=CN = briand, O = dev, O = example.org
  # brian.crt created
  
  # ---> briand.crt # add user to cluster
  kubectl config set-credentials briand --client-certificate=briand.crt --client-key=briand.key
  User "briand" set
  # briand user is set in minkube config
  
  # check for user briand
  # using vi ~/.kube/config results in:
  	# - name: briand
  	#     user:
  	#       client-certificate: /home/briandanks/gdrive_local/Learning/Learn_Kubernetes/k8s-training/Kubernetes-master/resources/rbac/briand.crt
  	#       client-key: /home/briandanks/gdrive_local/Learning/Learn_Kubernetes/k8s-training/Kubernetes-master/resources/rbac/briand.key
  # look for new user briand
  
  # provide a context of briand-minikube (briand into minikube)
  kubectl config set-context briand-minikube --cluster=minikube --user=briand --namespace=default
  Context "briand-minikube" created.
  # using vi ~/.kube/config results in:
  	#- context:
  	#    cluster: minikube
  	#    namespace: default
  	#    user: briand
  	#  name: briand-minikube
  
  # a check:
  kubectl config get-contexts
  CURRENT   NAME              CLUSTER    AUTHINFO   NAMESPACE
            briand-minikube   minikube   briand     default
  *         minikube          minikube   minikube   default
  
  # kubectl config use-context briand-minikube  # to set the context of the cluster
  
  # now the user briand is a valid user AND nothing else
  
  # alternative method    	# BEST PRACTICE
  openssl genpkey -out briand.key -algorithm ed25519
  cat briand.csr | base64 | tr -d "\n"  # to get the base64 encoded csr
  kubectl apply -f createuser.yaml
  certificate approve briand
  certificatesigningrequest.certificates.k8s.io/briand approved  # outcome message
  kubectl get csr/briand -o jsonpath='{.status.certificate}' | base64 -d > briand.crt 
  cp ~/.kube/config brian-kubeconfig.yaml  # whereever your yaml file are!
  	# cull all info except for relevant cluster e.g minikube or k3d-kubefirst etc.
  kubectl --kubeconfig briand-kubeconfig config set-credentials briand --client-key=briand.key --client-certificate=briand.crt --embed-certs=true
  User "briand" set.   # outcome
  kubectl --kubeconfig briand-kubeconfig config set-context briand --cluster=minikube --user=briand
  Context "briand" created.
  
  ```
-
- ## Other
- ==*Tip:*==
	- use `wc -l nginx-pod.yaml`to count lines of output - e.g. pod.yaml
-
- ## To define a role for a new user
- ```cmake
  # as per the role.yaml the
  # verbs: [""@get", "watch", "list"] #limit the access/actions for a user
  # from: 
  kubectl api-resources -o wide | rg pod
  # result in create,delete,deletecollection,get,list,patch,update,watch choices
  
  kubectl apply -f role.yaml
  role.rbac.authorization.k8s.io/pod-reader created
  # check
  kubectl get roles
  NAME         CREATED AT
  pod-reader   2023-07-05T12:10:35Z
  # user role is now defined
  
  ```
-
- ## To define the rolebinding (when the user, has a role defined)
- ```cmake
  # as per the role-binding.yaml
  kubectl apply -f role-binding.yaml
  rolebinding.rbac.authorization.k8s.io/read-pods created
  # user can now read-pods ["get", "watch", "list"]
  
  kubectl config use-context briand-minikube
  Switched to context "briand-minikube".
  
  # now get pods
  kubectl get pods
  # see nginx running
  
  kubectl config use-context minikube
  
  # new namespace created
  kubectl create ns test             
  namespace/test created
  
  kubectl  run nginx --image=nginx -n test
  pod/nginx created
  
  config use-context briand-minikube
  Switched to context "briand-minikube".
  
  # Note: the rolebing id limited to the appropriate namespace ---> kubectl get pod -n test will not be found
  
  ```
-
- *==Note:==* Role and RoleBinding is always limited to a namespace
- To get around this leverage cluster level means all resources in all namespaces are visible
- ```cmake
  # Leverage the cluster rolebinding # cluster-role.yaml AND cluster-role-binding.yaml
  kubectl config use-context minikube
  Switched to context "minikube".
  
  # create cluster role
  kubectl apply -f cluster-role.yaml
  clusterrole.rbac.authorization.k8s.io/pod-reader created
  # followed by cluster-role-binding
  apply -f cluster-role-binding.yaml
  clusterrolebinding.rbac.authorization.k8s.io/pod-reader-global created
  
  apply -f cluster-role-binding.yaml
  clusterrolebinding.rbac.authorization.k8s.io/pod-reader-global created
  
  kubectl get pod -n test
  NAME    READY   STATUS    RESTARTS   AGE
  nginx   1/1     Running   0          12m
  # Note: the namespace test pods are now visible as cluster role and role binding  Carefull!!
  # This now the case that briand is the same as default admin rights (in context to permissions)
  ```
-
- For all users:
- *==Note:==* the openssl creta csr we nominated briand to be member of O=dev (which is a group) and the group dev is in the cluster-role-binding.yaml the anyone belonging to group O=dev can inherit permissions
-
### Service accounts
- Every namespace created has a service-account created as default
- ```cmake
  kubectl get sa -n test
  NAME      SECRETS   AGE
  default   0         49m
  
  # create a serviceaccount in namespace test
  kubectl create sa test-sa -n test
  kubectl create sa test-sa
  
  # check if serviceaccount is in namespace
  kubectl get sa -n test
  NAME      SECRETS   AGE
  default   0         51m
  test-sa   0         4s
  
  # create pod with serviceaccount
  kubectl apply -f kubectl-pod.yaml 
  pod/kubectl-pod created
  
  kubectl auth can-i create pods --as="system:serviceaccount:default:test-sa"
  no
  # due to the limitations of the role and
  kubectl auth can-i get pods --as="system:serviceaccount:default:test-sa"
  yes
  kubectl auth can-i get pods --as=system:serviceaccount:default:test-sa -n test
  no
  
  ```
-
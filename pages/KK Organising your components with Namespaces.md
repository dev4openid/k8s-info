- # Organising your components with K8s Namespaces (01:46:16)
  title:: KK Organising your components with Namespaces
- ## namespaces
- `kubectl config set-context --current --namespace=nginx`
	- is used to move from 'default' tp 'nginx' namespace
-
- ## K8s Namespaced Explained
  |Name |Status| Age| Comment|
  |--|--|--|--|
  |default |Active |12h | |
  |kube-node-lease |Active |12h |heartbeat of nodes |
  |kube-public|Active |12h |`kubectl cluster-info` will give you key info |
  |kube-system        |Active|12h| leave alone |
-
- Create namespace `kubectl create namespace my-namespace`  BUT better in configmap file!
- e.g.:
	- ```cmake
	  apiVersion: v1
	  kind: ConfigMap
	  metadata:
	    name: mongodb-configmap
	    namespace: my-namespace     # note this to ensure correct namespace is enforced
	  data:
	    database-url: mongodb-service
	  ```
-
- ## Usecase to use namespace
	- > associate types of resources in a group e.g. Database / Monitoring / Elastic Stack
	  Conflicts between teams, same application (but different deployment)
	  Staging vs Development using common "services"
	  Production "Blue" and "Green"
	  Team Access and Resource Limits on namespaces. Limit CPU/RAM/Storage by a team on a common resource ("out of balance between teams")
-
- ## Access Service in another namespace
	- Each namespace must have on configmap and/or secret to access common resource (e.g. database)
	- service can be common to more than one namespace
	- ```cmake
	  apiVersion: v1
	  kind: ConfigMap
	  metadata:
	    name: mongodb-configmap
	  data: 
	    database-url: mongodb-service.database   #  NOTE: the suffix  .database 
	                                             # to facilitate common usage between teams
	  ```
-
- ## Components that cannot be created in a namespace
	- vol
	- node
	- `kubectl api-resources --namespaced=false`
	- ```cmake
	  NAME                              SHORTNAMES   APIVERSION                             NAMESPACED   KIND
	  componentstatuses                 cs           v1                                     false        ComponentStatus
	  namespaces                        ns           v1                                     false        Namespace
	  nodes                             no           v1                                     false        Node
	  persistentvolumes                 pv           v1                                     false        PersistentVolume
	  mutatingwebhookconfigurations                  admissionregistration.k8s.io/v1        false        MutatingWebhookConfiguration
	  validatingwebhookconfigurations                admissionregistration.k8s.io/v1        false        ValidatingWebhookConfiguration
	  customresourcedefinitions         crd,crds     apiextensions.k8s.io/v1                false        CustomResourceDefinition
	  apiservices                                    apiregistration.k8s.io/v1              false        APIService
	  tokenreviews                                   authentication.k8s.io/v1               false        TokenReview
	  selfsubjectaccessreviews                       authorization.k8s.io/v1                false        SelfSubjectAccessReview
	  selfsubjectrulesreviews                        authorization.k8s.io/v1                false        SelfSubjectRulesReview
	  subjectaccessreviews                           authorization.k8s.io/v1                false        SubjectAccessReview
	  certificatesigningrequests        csr          certificates.k8s.io/v1                 false        CertificateSigningRequest
	  flowschemas                                    flowcontrol.apiserver.k8s.io/v1beta3   false        FlowSchema
	  prioritylevelconfigurations                    flowcontrol.apiserver.k8s.io/v1beta3   false        PriorityLevelConfiguration
	  ingressclasses                                 networking.k8s.io/v1                   false        IngressClass
	  runtimeclasses                                 node.k8s.io/v1                         false        RuntimeClass
	  clusterrolebindings                            rbac.authorization.k8s.io/v1           false        ClusterRoleBinding
	  clusterroles                                   rbac.authorization.k8s.io/v1           false        ClusterRole
	  priorityclasses                   pc           scheduling.k8s.io/v1                   false        PriorityClass
	  csidrivers                                     storage.k8s.io/v1                      false        CSIDriver
	  csinodes                                       storage.k8s.io/v1                      false        CSINode
	  storageclasses                    sc           storage.k8s.io/v1                      false        StorageClass
	  volumeattachments                              storage.k8s.io/v1                      false        VolumeAttachment
	  ```
	- `kubectl api-resources --namespaced=false` does the opposite in these can be used in any namespace
- *==Note:==* use ==kubens== to change default from "default" to the namespace you have created; use `brew install kubectx`
-
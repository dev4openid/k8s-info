- # Stateful Service (STS)
- >each pod will connect to it's own PVC and PV
  >but service is NOT LoadBalancer but None (i.e. a Headless Service) ---> clusterIP: None
  >all pods are ordered pods with sticky ID (to ensure consistency and allow slaves/master to find each other for replication)
  >only master is read/write - slaves are read only
  >if the ordered sequence of pods has a problem with any node the the process stops and no further pods are initiated (sequence dependency in the order)
  >e.g.
  >>mongodb-0.mongodb-svc.default.svc.cluster.local:27017   (coreDNS reference)
  >>*==Note:==*
  >mongodb-0 is the pod name plus a -increment (e.g. -0 and so forth)
  >mongodb-svc is the service name
  >default is the minikube default or could be any namespace
- ![Deployment vs. Statefulset](/home/briandanks/Pictures/Screenshots/Screenshot from 2023-07-04 10-51-40.png){:height 220, :width 650}
- Deployment vs. Statefulset
- The pods are now sequence **BUT** need to set up replicaset to ensure data is consistent from master to slaves
	- >`kubectl exec -it mongo-0 -- mongo`
	  >then in mongo at prompt execute
	  >```json
	  rs.initiate(
	  	{
	      _id:"rs0",	# rs0 is the replicaset name
	        members: [
	          {_id:0, host : "mongo-0.mongo.default.svc.cluster.local:27017"},
	          {_id:0, host : "mongo-1.mongo.default.svc.cluster.local:27017"},
	          {_id:0, host : "mongo-2.mongo.default.svc.cluster.local:27017"}
	        ]
	      }
	  )
	  ```
	- then exit and reenter, look for `rs.status()`and check the prompt is rs0:PRIMARY (this can be checked for rs1:SECONDARY or rs2 :SECONDARY)
	- goto `kubectl exec -it mongo-1 -- mongo` and execute `rs.slaveOk()`to invoke the sync of data from master to slaves
-
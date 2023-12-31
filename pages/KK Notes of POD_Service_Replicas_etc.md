- *==Notes:==*
- To create a pod run the following: ==`kubectl run redis --image=redis -n=finance`==
- `kubectl set image rs new-replica-set *=busybox --dry-run=client`
- `kubectl scale rs new-replica-set  --replicas=5 --dry-run=client`
- `kubectl create deployment --image=nginx nginx --dry-run=client -o yaml > nginx-deployment.yaml`
- `kubectl create deployment nginx --image=nginx --replicas=4 --dry-run=client -o yaml > nginx-deployment.yaml `
- Generate Deployment with 4 Replicas - `kubectl create deployment nginx --image=nginx --replicas=4`
- scale a deployment using `kubectl scale deployment nginx --replicas=4`
- replace a pod example `kubectl replace --force -f nginx.yaml`
- Create a Service named redis-service of type ClusterIP to expose pod redis on port 6379 - `kubectl expose pod redis --port=6379 --name=redis-service --dry-run=client -o yaml`
- OR `kubectl create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml` (This will not use the pods labels as selectors, instead it will assume selectors as app=redis.
- Create a Service named nginx of type NodePort to expose pod nginx's port 80 on port 30080 on the nodes: `kubectl expose pod nginx --type=NodePort --port=80 --name=nginx-service --dry-run=client -o yaml` (This will automatically use the pod's labels as selectors, [but you cannot specify the node port](https://github.com/kubernetes/kubernetes/issues/25478)
- OR `kubectl create service nodeport nginx --tcp=80:80 --node-port=30080 --dry-run=client -o yaml` (This will not use the pods labels as selectors)
- *==Note:==* you can create a pod and service at the same time: `kubectl run http --image=httpd:alpine --port=80 --expose=true`
- AND use kubectl options -h for options applicable to all commands
- Controllers - i.e. Deployments / ReplicaSets / StatefulSets / etc.  need to have the template: cue and the spec has:
- ```yaml
  spec:
    replicas: 3
    selector: 
      matchLabels:
        app: myapp 
  ```
-
- selector: --->  matchLabels: which must match the template: ---> metadata: ---> labels:
- ```yaml
  spec:
    replicas: 3
    selector:
      matchLabels:
        app: nginx-deployment	# this one aND
    template:
      metadata:
        labels:
          app: nginx-deployment # this one
      spec:
        containers:
        - name: nginx
          image: nginx:1.20.2
          ports:
          - containerPort: 80
  
  ```
-
- as found in e.g.
- ```yaml
  ```
-
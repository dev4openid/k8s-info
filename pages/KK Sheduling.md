- # Scheduling
### Manual scheduling
- For e.g. of nginx: - Pod Definition
- ```yaml
  apiVersion: v1
  kind: Pod
  metadata:
    name: nginx
    labels:
      name: nginx
  spec:
    containers:
      - name: nginx
        image: nginx
        ports:
          - containerPort: 80
    node: node01			# simplest method, then delete and apply to create pod
  
  ```
-
- create a pod Binding definition
- ```yaml
  apiVersion: v1
  kind: Binding
  metadata:
    name: nginx
  
  target:
    apiVersion: v1
    kind: Node
    name: node01
  ```
-
- converted to JSON
- ```json
  ```
- So in e.g.:
- ```cmake
  curl --header "Content-Type: application/json" --request POST --data
  '{
    "apiVersion": "v1",
    "kind": "Binding",
    "metadata": {
      "name": "nginx"
    },
    "target": {
      "apiVersion": "v1",
      "kind": "Node",
      "name": "node01"
    }
  }' http://$SERVER/api/v1/namespaces/dafault/pods/$PODNAME/binding
    # http://$SERVER/api/v1/namespaces/dafault/pods/node01/binding
    #  but how to resolve $SERVER    ????????
  ```
-
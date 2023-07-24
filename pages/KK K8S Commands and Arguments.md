- # K8s Commands and Arguments
  title:: KK K8S Commands and Arguments
- For kubernetes `kubectl apply -f pod-definition.yaml`
- ```cmake
  apiVersion: v1
  kind: Pod
  metadata:
  	name: ubuntu-sleeper-pod
  spec:
  	containers:
      - name: ubuntu-sleeper
        image: ubuntu-sleeper
        command:
        	- sleep2.0
        	- "10"
        OR
        command: ["sleep"]
        args: ["15"]
        OR
        command: ["sleep", "20"]
  ```
-
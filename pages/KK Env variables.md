- # K8S Env variables
  title:: KK Env variables
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
        env:
        	- name: environ_value
             value: "blue"
  
  ```
-
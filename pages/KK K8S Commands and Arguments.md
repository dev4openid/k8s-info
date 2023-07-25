- # From Docker
- From docker `docker run ubuntu sleep 5` # NoteOR creat a dockerfile FROM ubuntu CMD sleep CMD 5 OR ["sleep", "5]"
- OR FROM ubuntu ENTRYPOINT 10 # becomes docker run ubuntu-sleeper 10
- OR FROM ubuntu ENTRYPOINT ["sleep"] CMD ["5"] # defaults if parameter of 10 **or** is forgotten
- OR ENTRYPOINT can be overridden by a second instance of ENTRYPOINT ["sleep2.0"]
- ```
      # docker example
              docker run --name ubuntu-sleeper \
              	--entrypoint sleep2.0
                  ubuntu-sleeper 10
    ```
-
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
- Application Command
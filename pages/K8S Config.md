- # K8S Config
- For kubernetes `kubectl apply -f pod-definition.yaml`
- ![Configmaps methods](/home/briandanks/Pictures/Screenshots/Screenshot from 2023-07-20 18-06-04.png)
-
-
- ```yaml
  spec:
    containers:
    - env:
      - name: APP_COLOR
        valueFrom:
          configMapKeyRef:
            name: webapp-config-map
            key: APP_COLOR
  ```
- OR
- ```yaml
  spec:
    containers:
    - envFrom: 
          configMapRef:
            name: webapp-config-map
  ```
- Also a CLI version is: `kubectl create configmap webapp-config-map --from-literal=APP_COLOR=darkblue`
-
-
-
- *==Note:==* Do NOT forget
- `kubectl replace --force -f new-pod-defintion.yaml    # replace an existing pod`
-
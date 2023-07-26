- # Secrets
  title:: KK Secrets
- ![Imperative Secrets](/home/briandanks/Pictures/Screenshots/Screenshot from 2023-07-20 20-33-09.png){:height 360, :width 650}
- Imperative Secrets
  id:: f4655dab-7e1d-494f-bed1-da4ecfb0f3d9
- ![Declarative Secrets](/home/briandanks/Pictures/Screenshots/Screenshot from 2023-07-20 20-36-10.png){:height 336, :width 648}
- Declarative Secrets
- ![Encrypt Secret (Data Row iteratively)](/home/briandanks/Pictures/Screenshots/Screenshot from 2023-07-20 20-38-02.png){:height 426, :width 650}
-
- Encrypt Secret (Data Row iteratively)
- Examples:
- ```yaml
  apiVersion: v1
  data:
    DB_Host: c3FsMDE=
    DB_Password: cGFzc3dvcmQxMjM=
    DB_User: cm9vdA==
  kind: Secret
  metadata:
    creationTimestamp: "2023-07-21T12:05:13Z"
    name: db-secret
    namespace: default
    resourceVersion: "988986"
    uid: d4fd2af7-46fc-4b2e-9713-b126d77c1714
  type: Opaque
  ```
- above is db-secret.yaml
- on CLI: `kubectl create secret generic db-secret --from-literal=DB_Host=sql01 --from-literal=DB_User=root --from-literal=DB_Password=password123`
-
- How to reference Secrets from Pod
- ```yaml
  spec:
    containers:
    - name: simple-webapp-color
      image: simple-webapp-color
      ports:
      - containrePort: 8080
      envFrom:
      - secretRef:
          configMapKeyRef:
             name: app-secret
  ```
- from a source like secret-data.yaml:
- ```yaml
  apiVersion: v1
  kind: Secret
  metadata:
     name: app-secret
  data:
    DB_HOST: dsfdAasdf=
    DB_User:  CM9vA==
    DB_Password: cGFassd4F
  ```
- *==Note:==* Best practice to encrypt all fields the where / who / password
- Methods of storing Secrets:
- ![Methods of storing Secrets](/home/briandanks/Pictures/Screenshots/Screenshot from 2023-07-20 20-49-56.png){:height 525, :width 650}
- Methods of storing Secrets
- ![Each element in Secrets are stored in different files in Volumes](/home/briandanks/Pictures/Screenshots/Screenshot from 2023-07-20 20-50-38.png)
- Each element in Secrets are stored in different files in Volumes
- *==Notes:==* The Secrets are NOT in Git/Github    AND are stored in etcd !!! Use Vault instead
-
- Exmple of Pod-Definition
- ```yaml
  spec
    containers
      env:
        - name: DB_Host
          valueFrom:
            configMapKeyRef:
              name: db-secret
              key: DB_Host
        - name: DB_Password
          valueFrom:
            configMapKeyRef:
              name: db-secret
              key: DB_Password
        - name: DB_User
          valueFrom:
            configMapKeyRef:
              name: db-secret
              key: DB_User
  ```
-
- Example of Pod-Definition
- ```yaml
  spec
    containers
    	- envFrom:
    		- secretRef:
              name: db-secret		# db-secret yaml file
  ```
-
- [[Notes: Secrets and ConfigMaps]]
-
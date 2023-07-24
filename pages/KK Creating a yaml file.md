- # Creating a yaml file
  title:: KK Creating a yaml file
- Firstly there is always a Deployment and a Service yaml file (Need both)
	- Deployment to define what is to be instantiated
	- Service is to define how the Deployment is to be accessed
- ![Metadata](/home/briandanks/Pictures/Screenshots/Screenshot from 2023-06-20 13-38-12.png)
- Metadata
- ![Specification](/home/briandanks/Pictures/Screenshots/Screenshot from 2023-06-20 13-42-30.png)
- Specification for Deployment and/or Service
- ![Deployment and/or Service](/home/briandanks/Pictures/Screenshots/Screenshot from 2023-06-20 13-44-11.png)
- Deployment and Service files (could include Mounting etc.)   Note the apiversion DIFFERENCE in format!
- ![image.png](../assets/image_1686861013734_0.png)
- Attributes of "spec" are specific to kind of file (Deployment vs. Service)
- 3 parts!
	- 1. metadata
	  2. specification
	  3. status (Notice: automatically generated on instatiation by k8s)
- Note: all status is found in etcd
-
- ![image.png](../assets/image_1686905575254_0.png)
- Note: the concept of spec within a spec  - this is the actual deployable config - same goes for the service spec
- ==etcd provides the "defaults" for all Deployments/Services==
- ## Blueprint for Pods (Templates)
- ==Structure of yaml file:==
	- ```yaml
	  apiVersion:
	  kind:
	  metadata:
	  spec:
	  ```
- *==Tip:==*
	- use `kubectl api-resources | grep deployment`  ---> (or service /  secret / configmap / pods)
### Template
- ![Pod Specification](/home/briandanks/Pictures/Screenshots/Screenshot from 2023-06-20 15-43-01.png)
- Pod Specification
-
- ### Blueprint for Pods (Templates)
- ==Structure of yaml file:==
	- ```yaml
	  apiVersion:
	  kind:
	  metadata:
	  spec:
	  ```
- *==Tip:==*
	- use `kubectl api-resources | grep deployment`  ---> (or service /  secret / configmap / pods)
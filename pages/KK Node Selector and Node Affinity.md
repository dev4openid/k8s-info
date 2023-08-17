- # Node Selector and Node Affinity
  title:: KK Node Selector and Node Affinity
- ## Affinity Summary
- ![Affinity methods](/home/briandanks/Pictures/Screenshots/Screenshot from 2023-07-04 20-03-00.png)
  id:: 96fff468-db80-49f9-9c48-4853f9b9bfd7
- Affinity methods
### Node Selector
- Simple model means labelling the node to get the desired effect
- `kubectl label node <node-name> <Label-key>=<label-value>`, an e.g. `kubectl label node node01 size=Large` thus the pod now has nodeSelector: of size: Large
-
### Node Affinity
- In pod definition:
- ```yaml
  apiVersion: v1                                    
  kind: Pod                                         
  metadata:                                         
    name: nginx                                     
  spec:                                             
    containers:                                     
    - name: nginx                                   
      image: nginx:1.20.2                           
      ports:                                        
      - containerPort: 80                           
    affinity:                                       
      requiredSuringSchedulingIgnoreDuringExecution:          
        nodeSelectorTerms:                          
        - matchExpressions:                         
          - key: size                               
            operator: In  # NotIn alternative                 
            values:                                 
            - Large                                 
              Medium   # to add additional node - gives choice
                                                    
  # OR we can use:                                  
                                                    
    affinity:                                       
      requiredSuringSchedulingIgnoreDuringExecution:
        nodeSelectorTerms:                          
        - matchExpressions:                         
          - key: size                               
            operator: Exists   # or NotExists ?????
  
  ```
- Types of node affinity
	- > requiredDuringSchedulingIgnoreDuringExecution
	  preferredDuringSchedulingIgnoreDuringExecution
	  *AND* soon
	  requiredSuringSchedulingIRequiredDuringExecution
- Therefore for 3 Affinity types:
- ||DuringScheduling|DuringExecution|
  |--|--|--|
  |Type 1|Required|Ignored|
  |Type 2|Preferred|Ignored|
  |Type 3|Required|Required|
-
-
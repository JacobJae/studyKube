### pod definition file
eg. pod-definition.yml
```
apiVersion:
kind:
metadata:



spec:
```
- Kubernetes definition file always has these 4 top-level fields (top level or root level properties)
  - API version: version of Kubernetes API version
  - Kind: refers to the type of object we are trying to create
  - Metadata: data about the object like its name labels etc...
    - You can only specify metadata that Kubernetes expects, no custom metadata is acceptable
    - But under labels, you can have any kind of key or value pairs
  - Spec: this is where we would provide additional information to Kubernetes pertaining to that object

![image](https://github.com/JacobJae/studyKube/assets/38265255/ed6d14d4-6d05-4448-82d2-96586fc6b928)
You can see the details of pod using `kubectl describe pod myapp-pod`

### Pods
- `kubectl get pods` list pods
- `kubectl get pods -o wide` list pods with node
- `kubectl run nginx --image=nginx` create pod
- `kubectl describe pod < pod name>` see pod
  - You can check Events section to see error message
- `kubectl delete pod <pod name>`
- `kubectl run <pod name> --image=< image name > --dry-run=client -o yaml` Creaete pod-definition file in YAML format
- `kubectl create -f <pod-definition yml file name>`

### Controller
- Replication controller
  - Replication controller helps us run multiple instances of a single pot in the Kubernetes cluster
  - Provide High Availability
  - It make sure specified number of pods running all the time
  - Load balance when the user increases
  - scale when user increases
  - ![image](https://github.com/JacobJae/studyKube/assets/38265255/30fc96ba-4d94-4809-ba0e-3e899086fc2c)
  - Replication Controller(old way) and Replica Set(new way) have the same purpose but they are not the same
  - Add pod-definition under template, except for `apiVersion` and `kind`
  - ![image](https://github.com/JacobJae/studyKube/assets/38265255/5c1cf418-fed2-4f83-9aee-a66a8d8a08a7)
- Replica Set
  - role of the replica set is to monitor the pods and if any of them were to fail deploy new ones
  - Difference: `apiVersion` is `apps/v1`
  - Difference: requires **selector** definition (it has be to present in definition for replica set)
    - The selector section helps the replica set identify what parts fall under it
    - Why? replica set can also manage parts that were not created as part of the replica set creation
    - replication controller also can use selector, if not specified, it assumes it to be the same as the labels provided in the port definition file
  - ![image](https://github.com/JacobJae/studyKube/assets/38265255/4bb4b54a-79f5-4057-8f93-3c3d29bf1ce8)
  - Labels and Selectors
    - Labels are uesd by Replica Set to which pod needs to be monitored (not sure about this concept) 
  - Scale
    1. Change number of pods by editing `replicas` and run `kubectl replace -f < replica set definition file >.yml`
    2. Run scale command, `kubectl scale --replicas=6 -f < replica set definition file >.yml`
    3. Run scale command with type and name `kubectl scale --replicas=6 replicaset < replica set name >`
    > Note that if you use scale command, definition file used as input will not change the value inside definition file
  - commands
    - `kubectl create -f replicaset-definition.yml`
    - `kubectl get replicaset`
    - `kubectl delete replicaset myapp-replicaset`
    - `kubectl replcase -f replicaset-definition.yml`
    - `kubectl scale --replicas=6 -f replicaset-definition.yml`














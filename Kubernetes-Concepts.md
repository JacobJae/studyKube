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

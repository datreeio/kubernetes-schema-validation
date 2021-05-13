# misconfigs
This dir contains seven Kubernetes manifest files with a different misconfiguration in each one:  

### api-deprecation.yaml
**wrong:** `apiVersion: apps/v1beta2`  
**correct:** `apiVersion: apps/v1`  
**reason:** `apps/v1beta2` was deprecated for resource type "Deployment" in Kuberenetes version 1.18.0  

### invalid-kind-value.yaml
wrong: `kind: pod`  
correct: `kind: Pod`  
reason: resource type must start with a capita letter - `Pod`  

### invalid-label-value.yaml
wrong: `owner: ---`  
correct: `owner: frodo-baggins`  
reason: labels values must start and end with an alphanumeric letter

### invalid-protocol-type.yaml
wrong: `protocol: 22`  
correct: `protocol: TCP`  
reason: protocol type must be a string

### invalid-spec-key.yaml
wrong: `Spec:`  
correct: `spec:`  
reason: `spec` must start with a small s'

### missing-image.yaml
wrong:  
```yaml
containers:
    - name: web
```  
correct:
```yaml
containers:
    - name: web
      image: nginx
```  
reason: each container must include an image name

### wrong-k8s-indentation.yaml
wrong:  
```yaml
spec:
containers:
  - name: web
    image: nginx
    ports:
      - name: web
        containerPort: 80
        protocol: TCP
```
correct:  
```yaml
spec:
  containers:
  - name: web
    image: nginx
    ports:
    - name: web
      containerPort: 80
      protocol: TCP
```  
reason: Kuberenetes\YAML indentation requires one tab space when listing `containers` 

# benchmark
This dir contains 100 valid Kubernetes manifest files.  
All files are containing the same Kubernetes configurations. 
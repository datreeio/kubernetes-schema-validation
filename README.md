# misconfigs
This dir contains seven Kubernetes manifest files with a different misconfiguration in each one:  

### [api-deprecation.yaml](https://github.com/datreeio/kubernetes-schema-validation/blob/main/misconfigs/api-deprecation.yaml#L1)
**wrong:** `apiVersion: apps/v1beta2`  
**correct:** `apiVersion: apps/v1`  
**reason:** `apps/v1beta2` was deprecated for resource type "Deployment" in Kuberenetes version 1.18.0  

### [invalid-kind-value.yaml](https://github.com/datreeio/kubernetes-schema-validation/blob/main/misconfigs/invalid-kind-value.yaml#L2)
**wrong:** `kind: pod`  
**correct:** `kind: Pod`  
**reason:** resource type must start with a capita letter - `Pod`  

### [invalid-label-value.yaml](https://github.com/datreeio/kubernetes-schema-validation/blob/main/misconfigs/invalid-lable-value.yaml#L6)
**wrong:** `owner: ---`  
**correct:** `owner: frodo-baggins`  
**reason:** labels values must start and end with an alphanumeric letter

### [invalid-protocol-type.yaml](https://github.com/datreeio/kubernetes-schema-validation/blob/main/misconfigs/invalid-protocol-type.yaml#L14)
**wrong:** `protocol: 22`  
**correct:** `protocol: TCP`  
**reason:** protocol type must be a string

### [invalid-spec-key.yaml](https://github.com/datreeio/kubernetes-schema-validation/blob/main/misconfigs/invalid-spec-key.yaml#L7)
**wrong:** `Spec:`  
**correct:** `spec:`  
**reason:** `spec` must start with a small s'

### [missing-image.yaml](https://github.com/datreeio/kubernetes-schema-validation/blob/main/misconfigs/missing-image.yaml#L9)
**wrong:**  
```yaml
containers:
    - name: web
```  
**correct:**
```yaml
containers:
    - name: web
      image: nginx
```  
**reason:** each container must include an image name

### [wrong-k8s-indentation.yaml](https://github.com/datreeio/kubernetes-schema-validation/blob/main/misconfigs/wrong-k8s-indentation.yaml#L8-L14)
**wrong:**  
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
**correct:**  
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
**reason:** Kuberenetes\YAML indentation requires one tab space when listing `containers` 

# benchmark
This dir contains 100 valid Kubernetes manifest files.  
All files are containing the same Kubernetes configurations. 
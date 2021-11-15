# About this reposiroty
This repository contains resources for the blog post:  
"[A Deep Dive Into Kubernetes Schema Validation](https://datree.io/resources/kubernetes-schema-validation/?utm_source=github&utm_medium=schema_validation_repo)"

# Misconfigs
This dir contains seven Kubernetes manifest files, each with a different misconfiguration:  

### [api-deprecation.yaml](https://github.com/datreeio/kubernetes-schema-validation/blob/main/misconfigs/api-deprecation.yaml#L1)
**wrong:** `apiVersion: apps/v1beta2`  
**correct:** `apiVersion: apps/v1`  
**reason:** `apps/v1beta2` was deprecated for resource type "Deployment" in Kubernetes version 1.18.0

### [invalid-kind-value.yaml](https://github.com/datreeio/kubernetes-schema-validation/blob/main/misconfigs/invalid-kind-value.yaml#L2)
**wrong:** `kind: pod`  
**correct:** `kind: Pod`  
**reason:** resource type must start with a capital letter - `Pod`

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
**reason:** `spec` must start with a small 's'

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
**reason:** Kubernetes\YAML indentation requires one tab space when listing `containers`

## Misconfigurations coverage summary

[![misconfigurations-coverage](https://raw.githubusercontent.com/datreeio/kubernetes-schema-validation/main/images/comparing-table.png)](#) 

# Benchmark
This dir contains 100 valid Kubernetes manifest files.  
All files contain the same Kubernetes configuration. 

[![benchmark-results](https://raw.githubusercontent.com/datreeio/kubernetes-schema-validation/main/images/benchmark-test-results.png)](#) 

# Commands
### running schema validation tests
**kubeval:** `kubeval --strict misconfigs/*.yaml -v "1.18.0"`  
**kubeconform:** `kubeconform -strict misconfigs/*.yaml`  
**kubectl dry-run in client mode:** `kubectl apply -f misconfigs/ --dry-run=client`  
**kubectl dry-run in server mode:** `kubectl apply -f misconfigs/ --dry-run=server`  

### Running benchmark tests
:wrench: prerequisite - [hyperfine](https://github.com/sharkdp/hyperfine) installed  

**kubeval:** `hyperfine --warmup 5 'kubeval --strict benchmark/*.yaml -v "1.18.0"'`  
**kubeconform:** `hyperfine --warmup 5 'kubeconform -strict benchmark/*.yaml'`  
**kubectl dry-run in client mode:** `hyperfine --warmup 5 'kubectl apply -f benchmark/ --dry-run=client'`  
**kubectl dry-run in server mode:** `hyperfine --warmup 5 'kubectl apply -f benchmark/ --dry-run=server'`  

# Resources
* My article about [K8s schema validation](https://dev.to/datreeio/a-deep-dive-into-kubernetes-schema-validation-39ll)
* Open an issue [here](https://github.com/datreeio/kubernetes-schema-validation) if you have any questions on this topic (k8s schema)
* kubectl --dry-run=client bug - [kubernetes/issues/51475](https://github.com/kubernetes/kubernetes/issues/51475)
* [Datree's CLI tool](https://github.com/datreeio/datree) to ensure K8s manifests and Helm charts follow best practices
* How to check CRDs and schema with Datree - [docs](https://hub.datree.io/schema-validation)

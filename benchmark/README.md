# benchmark
This dir contains 100 valid Kubernetes manifest files.  
All files contain the same Kubernetes configuration.  

[![benchmark-results](https://raw.githubusercontent.com/datreeio/kubernetes-schema-validation/main/images/benchmark-test-results.png)](#) 

### running benchmark tests
:wrench: prerequisite - [hyperfine](https://github.com/sharkdp/hyperfine) installed  

**kubeval:** `hyperfine --warmup 5 'kubeval --strict benchmark/*.yaml -v "1.18.0"'`  
**kubeconform:** `hyperfine --warmup 5 'kubeconform -strict benchmark/*.yaml'`  
**kubectl dry-run in client mode:** `hyperfine --warmup 5 'kubectl apply -f benchmark/ --dry-run=client'`  
**kubectl dry-run in server mode:** `hyperfine --warmup 5 'kubectl apply -f benchmark/ --dry-run=server'`  

### Taints and Tolerations
      
```bash      
kubectl taint nodes node-name key=value:taint-effect

NoSchedule | PreferNoSchedule | NoExecute

example: kubectl taint nodes node1 app=blue:NoSchedule
```

```bash
 cat bee.yaml 
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: bee
  name: bee
spec:
  containers:
  - image: nginx
    name: bee
  tolerations:
  - key: "spray"
    operator: "Equal"
    value: "mortein"
    effect: "NoSchedule"
```
```bash
controlplane ~ ➜  kubectl describe node | grep Taint
Taints:             node-role.kubernetes.io/control-plane:NoSchedule
Taints:             <none>

controlplane ~ ➜  kubectl describe node node01 | grep Taint
Taints:             <none>

controlplane ~ ➜  kubectl taint node node01 spray=mortein:NoSchedule
node/node01 tainted

controlplane ~ ➜  kubectl describe node node01 | grep Taint
Taints:             spray=mortein:NoSchedule
```

## To Remove taint on node
```bash
kubectl taint node controlplane node-role.kubernetes.io/control-plane:NoSchedule-
```

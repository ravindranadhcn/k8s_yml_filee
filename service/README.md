
# Service Imperative commands

```bash
kubectl create service clusterip redis-service --tcp=6379:6379 --dry-run=client -o yaml
```

```json
apiVersion: v1
kind: Service
metadata:
  creationTimestamp: null
  labels:
    app: redis-service
  name: redis-service
spec:
  ports:
  - name: 6379-6379
    port: 6379
    protocol: TCP
    targetPort: 6379
  selector:
    app: redis-service
  type: ClusterIP
status:
  loadBalancer: {}
```
  
  
  
  ## It will create pod and service as well
  
```bash
  kubectl run httpd --image=httpd:alpine --port=80 --expose
```

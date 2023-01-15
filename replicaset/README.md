

kubectl delete rs replicaset-{1..2}
  
kubectl get pods   --no-headers=true | awk '{print $1}' | xargs kubectl delete pod
  
  
kubectl scale --replicas=5 rs/new-replica-set

kubectl get pods -o json

kubectl get rs -o=jsonpath='{.items[0]}'

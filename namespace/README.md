
kubectl create -f namespace.yml

kubectl create namespace prepord

kubectl config set-context $(kubectl config current-context) --namespace=dev

kubectl get pods --namespace=default 
kubectl get pods --namespace=prod

kubectl get pods --all-namespaces

compute-quota.yaml

apiVersion: v1
kind: ResourceQuota
metadata:
  name: compute-quota
  namespace: dev
spec:
  hard:
    pods: "10"
    requests.cpu: "4"
    requests.memory: 5Gi
    limits.cpu: "10"
    limits.memory: 10Gi


kubectl create -f compute-quota.yaml


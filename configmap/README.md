Environment Variables in K8s // docker run -e APP_COLOR=pink simple-webapp-color
```docker
apiVersion: v1
kind: Pod
metadata:
  name: simple-webapp-color
spec:
  contianers:
  - name: simple-webapp-color-pod
    image: simple-webapp-color
    ports:
      - containerPort: 8080
    env:
      - name: APP_COLOR
        value: pink
```

```docker
cat /root/webapp-color-3/Dockerfile2 
FROM python:3.6-alpine

RUN pip install flask

COPY . /opt/

EXPOSE 8080

WORKDIR /opt

ENTRYPOINT ["python", "app.py"]

CMD ["--color", "red"]
```
```bash
cat /root/webapp-color-3/
Dockerfile2              webapp-color-pod-2.yaml  

controlplane ~ ➜  cat /root/webapp-color-3/webapp-color-pod-2.yaml 
apiVersion: v1 
kind: Pod 
metadata:
  name: webapp-green
  labels:
      name: webapp-green 
spec:
  containers:
  - name: simple-webapp
    image: kodekloud/webapp-color
    command: ["python", "app.py"]
    args: ["--color", "pink"]
```



### Different ways of specifing ENV Value Types
```bash
env:                          //Plain key value
  - name: APP_COLOR
    value: pink

env:                          // from config-map
  - name: APP_COLOR
    valueFrom:
      configMapKeyRef:
env:                          // from secrets
  - name: APP_COLOR
    valueFrom:
      secretkeyRef:
```
```bash
kubectl create cm webapp-config-map --from-literal=APP_COLOR=darkblue

apiVersion: v1
kind: Pod
metadata:
  labels:
    name: webapp-color
  name: webapp-color
spec:
  containers:
  - env:
    - name: APP_COLOR
      valueFrom:
        configMapKeyRef:
          name: webapp-config-map
          key: APP_COLOR
    image: kodekloud/webapp-color
    imagePullPolicy: Always
    name: webapp-color
```

## ConfigMaps:::

APP_COLOR: blue
APP_MODE: prod


## 2 ways to create config map

# 1. Imperative way : 
```bash
syntax:
kubectl create configmap \
    <configmap-name> --from-literal=<key>=<value>
    
    
kubectl create configmap \
    app-config  --from-literal=APP_COLOR=blue \
                --from-literal=APP_MOD=prod

other way is:::
kubectl create configmap \
  <configmap-name> --from-file=<path-to-file>
  
kubectl create configmap  \
  app-config --from-file=app_config.properties
```

# 2. Declarative way : using definition file
## kubectl 
```bash
config-map.yaml
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  APP_COLOR: blue
  APP_MODE: prod
  
kubectl create -f config-map.yaml

kubectl get configmaps

kubectl describe configmap-name

```
## pod-dafinition.yaml
```bash
apiVersion: v1
kind: Pod
metadata:
  name: simple-webapp-color
  labels:
    name: simple-webapp-color
spec:
  containers:
  - name: simple-webapp-color
    image: simaple-webapp-color
    ports:
      - containerPort: 8080
    envFrom:
      - configMapRef:
          name: app-config

```

If you want to inject single value from config map
```bassh
env:
  - name: APP_COLOR
    valueFrom:
      configMapKeyRef:
        name: app-config
        key:  APP_COLOR
```
you can use volumes:

```bash
volumes:
- name: app-congig-volume
  configMap:
    name: app-config
```

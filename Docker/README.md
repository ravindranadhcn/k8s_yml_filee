# Dockerfile
```docker
FROM ubuntu
ENTRYPOINT ["sleep"]    --->  command:["sleep2.0"] in k8s pod

CMD ["5"]               --->  args["10"]  in k8s pod
```
```bash
docker build -t ubuntu-sleeper .

docker container run ubuntu-sleeper   // it will run with default commands i.e sleep 5

docker container run ubuntu-sleeper 10  // it will override cmd options in the docker file. i.e sleep 10
```

If you want to override ENTRY-POINT 
```bash
docker container run --entrypoint sleep2.0 ubuntu-sleeper 10

apiVersion: v1
kind: Pod
metadata:
  name: ubuntu-sleeper-pod
spec:
  containers:
    - name: ubuntu-sleeper-pod
      image: ubuntu-sleeper
      command: ["sleep2.0"]  //it will override entrypoint in the dockerfile
      args: ["10"]   // it will override cmd options in the docker file
``` 
 (or)
```bash
apiVersion: v1
kind: Pod 
metadata:
  name: ubuntu-sleeper-3
spec:
  containers:
  - name: ubuntu
    image: ubuntu
    command:
      - "sleep"
      - "1200"
```

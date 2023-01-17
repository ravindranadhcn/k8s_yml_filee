## Secrets
```bash
kubectl create secret generic <secret-name> --from-literal=<key>=<value> 

kubectl create secret generic \
        app-secret --from-literal=DB_Host=mysql \
                   --from-literal=DB_User=root  \
                   --from-literal=DB_Password=passwd
```                   

### Commands

docker run ubuntu .

docker ps -a 

docker run ubuntu sleep 5

###### inside the Ubuntu image 

### DOCKERFILE

FROM ubuntu

CMD sleep 5 ### or CMD ["Sleep", "5"]


docker run ubuntu-sleeper sleep 10 


#### Dockerfile
```Dockerfile
FROM ubuntu

ENTRYPOINT ["sleep"]
```

docker run ubuntu-sleeper 10 

#### Dockerfile

```Dockerfile
FROM ubuntu

ENTRYPOINT ["sleep"]

CMD ["5"]
```

docker run ubuntu-sleeper 

docker run --entrypoint sleep2.0 ubuntu-sleeper 10


#### Commands and Arguments
```yaml
apiVersion: v1
kind: Pod
metatdata: 
   name: ubuntu-sleeper-pod
   labels:
      tier: first-version
specs:
   containers:
    - name: ubuntu-sleeper
      image: ubuntu-sleeper
      command: ["sleep2.0"]
      args: ['10']
```

```yaml
apiVersion: v1
kind: Pod
metatdata: 
   name: ubuntu-sleeper-pod
   labels:
      tier: first-version
specs:
   containers:
    - name: ubuntu-sleeper
      image: ubuntu-sleeper
      command: 
       - "sleep"
       - "5000"
      args: ['10']
```

```Dockerfile
FROM python:3.6-alpine

RUN pip install flask

COPY . /opt/

EXPOSE 8080

WORKDIR /opt

ENTRYPOINT ["python", "app.py"]

CMD ["--color", "red"]
```

```yaml
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
    args: ["--color", "green"]
```

#### Environment variables

kubectl create configmap \
   app-config --from-literal=APP_COLOR=blue


kubectl get configmaps

kubectl describe configmaps


#### Secrets creation
##### Imperative Approach
```bash
kubectl create secret  generic
      <secret-name> --from-literal=<value>


kubectl create secret  generic \
      app-sql --from-literal=mysql

kubectl create secret  generic \
      app-sql --from-file=app_secret.properties

kubectl create secret docker-registry secret-tiger-docker \
  --docker-email=tiger@acme.example \
  --docker-username=tiger \
  --docker-password=pass1234 \
  --docker-server=my-registry.example:5000


kubectl create secret generic \
    db-secret  --from-literal=DB_Host=sql01 \
                --from-literal=DB_User=root  \
                --from-literal=DB_Password=password123

```                
##### Declarative Approach

echo -n 'mysql' | base64  ### to encode the password

kubectl create -f secrets.yml


kubectl get secrets

kubectl describe secrets 

kubectl describe secret app-secret -o yaml  


echo "cmds45t=' | base64 --decode # to  decode secrets

### secrets like environment variables can be use an ENV, Single ENV and as a Volume

ls /opt/app-secret-volumes # to see the secrets files
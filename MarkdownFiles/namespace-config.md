#### Namespace

kubectl get pods --namespace=kube-system

kubectl create -f service.yaml --namespace=dev

kubectl run redis --image=redis --namespace=dev

kubectl create namespace dev

kubectl config set-context $(kubectl config current-context) --namspace=dev

kubectl get pods

kubectl get pods --all-namespaces

kubectl create -f compute-quota.yaml

kubectl get namespaces


##### db-server.dev.svc.cluster.local


## Imperative and declarative 

#### imperative 


#### create objects

kubectl run --image=nginx nginx

kubectl run redis --image=redis:alpine --labels="tier=db"

kubectl run httpd --image=httpd:alpine --port=80 --expose=true

kubectl create deployment --image=nginx nginx

kubectl expose deployment nginx --port 80

kubectl create -f nginx.yaml

kubectl create deployment --image=nginx nginx --dry-run=client -o yaml

kubectl create deployment nginx --image=nginx --dry-run=client -o yaml > nginx-deployment.yaml

kubectl create deployment redis-deploy --image=redis --dry-run=client  --replicas=2 --namespace=dev-ns  -o yaml > deployment-replica-2.yaml

kubectl apply -f deployment-replica-2.yaml 

#### Update Objects

kubectl edit deployment nginx

kubectl scale deployment nginx --replicas=5

kubectl set image deployment nginx nginx=nginx:1.18

kubectl replace -f nginx.yaml

kubectl replace --force -f nginx.yaml

kubectl delete -f nginx.yaml


#### Declarative

### create 

kubectl apply -f nginx.yaml

kubectl apply -f /path/to/config-files


#### update
kubectl apply -f nginx.yaml

## Service 

kubectl expose pod redis --port=6379 --name redis-service --dry-run=client -o yaml

kubectl create service clusterip redis --tcp=6379:6379 --dry-run=client -o yaml

kubectl expose pod nginx --type=NodePort --port=80 --name=nginx-service --dry-run=client -o yaml

kubectl create service nodeport nginx --tcp=80:80 --node-port=30080 --dry-run=client -o yaml

kubectl expose pod httpd --type=ClusterIP --port=6379 --target-port=89 --name=httpd


kubectl apply -f service-httpd.yaml 
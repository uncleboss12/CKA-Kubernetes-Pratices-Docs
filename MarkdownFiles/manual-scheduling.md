### Manual binidng of pods to Nodes 

##### After creating a yaml binding fuile run the below lines to bind manually

```bash
curl --header "Content-Type:application/json" --request POST --data  '{"apiVersion": "v1", "kind": "Binding": .....}  https://$SERVER/api/v1/namespaces/default/pods/$PODNAME/binding


kubectl replace -f nginx.yaml

kubectl replace  --force -f nginx.yaml

kubectl get pods --selector app=APP1

kubectl get pods -l env=prod,bu=finance,tier=frontend --show-labels 

kubectl get pod -A

kubectl logs <pod-name> --name-space=<namespac-name>
```

### Taints and Tolerations
```bash
kubectl taint nodes node-name key=value:taint-effect

kubectl taint nodes node-name app=BlUE:taint:NoSchedule   # NoSchedule | PreferNoSchedule | NoExecute

kubectl describe node kubemaster | grep Taint

kubectl taint nodes kubemaster node-role.kubernetes.io/master-
# OR for newer versions:
kubectl taint nodes kubemaster node-role.kubernetes.io/control-plane-

#### to label nodes

kubectl label nodes <node-name> <label-key>=<label-value>


kubectl label nodes node1 size=Large
```

#### Daemon set 

kubectl get daemonsets

kubectl describe daemonsets monitoring-daemon

#### Static Pods

ls /etc/kubernetes/manifests

kubeconfig.yaml

kubelet.service

docker ps


#### Multiple Schedulers
```bash
kubectl describe pod kube-scheduler-controlplane  --namespace=kube-system 

kubectl get serviceaccount -n kube-system 

kubectl get clusterrolebinding

/root/my-scheduler-config.yaml 

...existing code...
```

```bash
# Create ConfigMap from scheduler config file
kubectl create configmap my-scheduler-config --namespace=kube-system --from-file=/root/my-scheduler-config.yaml

# Verify ConfigMap creation
kubectl get configmap my-scheduler-config
kubectl describe configmap my-scheduler-config
```


#### Admission Controllers

kube-apiserver -h | grep enable-admission-plugins

kubectl exec kube-apiserver-controlplane -n kube-system -- kube-apiserver -h | grep enable-admission-plugins  ## in kubeadm 

vi /etc/kubernetes/manifests/kube-apiserver.yaml 

ps -ef | grep kube-apiserver | grep admission-

##### Validating and Mutating Admission Controllers

kubectl create secret tls webhook-secret-tls \
  --cert=/root/keys/webhook-server-tls.crt \
  --key=/root/keys/webhook-server-tls.key \
  --namespace=webhook-demo



#### Monitoring -- metric Server

minikube addons enable metric-server

git clone https://github.com/kubernetes-incubator/metrics-server.git

Kubectl create -f deploy/1.8+/

kubectl top node   

kubectl top pod

kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml


 #### Managing application logs

docker run kodekloud/event-simulator

kubectl create -f event-simulator.yaml

kubectl logs -f event-simulator-pod

kubectl logs -f event-simulator-pod event-simulator  ## Multiple images in a pods

kubectl logs <pod-name>


#### Rolling Updates and Rollbacks

kubectl rollout status deployment/myapp-deployment

kubectl rollout history deployment/myapp-deployment

kubectl apply -f myapp-deployment.yaml

kubectl set image deployment/myapp-deployment \
         nginx-container=nginx:1.9.1

kubectl get replicasets

kubectl rollout undo  deployment/myapp-deployment

kubectl get replicasets

kubectl describe deployment frontend ## see the strategy

kubectl get deployment frontend -o yaml > deployment-frontend.yaml

kubectl set image deployment/frontend \
         simple-webapp=kodekloud/webapp-color:v3

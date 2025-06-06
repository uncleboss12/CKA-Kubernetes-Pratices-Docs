### for replicationcontroller

kubectl get pods

kubectl create -f replicacontroller.yaml

kubectl get replicationcontroller

kubectl get pods

### for replicaset

kubectl get pods

kubectl create -f replicaset.yaml

kubectl get replicaset

kubectl get replicaset -o wide

#### Scale
kubectl replace -f replicaset.yml

kubectl scale --replicas=6 -f replicaset.yml

kubectl scale --replicas=6 replicaset my-replicaset

kubectl edit replicaset new-replica-set

#####
 kubectl delete replicaset my-replicaset
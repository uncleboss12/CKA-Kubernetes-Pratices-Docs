### NodePort-Service

kubectl create -f service.yaml

kubectl get services

curl hhtp:/192.168.1.2:30008


### ClusterIP-Service

kubectl create -f service-clusterip.yaml

kubectl get services

curl hhtp:/192.168.1.2:30008


### Loadbalancer-Service

## DNS 

kubectl run busybox --rm -it --image=busybox:1.28 -- nslookup nginx-resolver-service

kubectl run busybox --rm -it --image=busybox:1.28 -- nslookup nginx-resolver-service > /root/CKA/nginx.svc

kubectl run busybox --rm -it --image=busybox:1.28 -- nslookup nginx-resolver

kubectl run busybox --rm -it --image=busybox:1.28 -- nslookup nginx-resolver > /root/CKA/nginx.pod

cat /root/CKA/nginx.svc
cat /root/CKA/nginx.pod

kubectl run nginx-resolver --image=nginx
kubectl expose pod nginx-resolver --name=nginx-resolver-service --port=80 --target-port=80 --type=ClusterIP

kubectl run test-nslookup --image=busybox:1.28 --rm -it --restart=Never -- nslookup nginx-resolver-service
kubectl run test-nslookup --image=busybox:1.28 --rm -it --restart=Never -- nslookup nginx-resolver-service > /root/CKA/nginx.svc


kubectl get pod nginx-resolver -o wide
kubectl run test-nslookup --image=busybox:1.28 --rm -it --restart=Never -- nslookup <P-O-D-I-P.default.pod> > /root/CKA/nginx.pod

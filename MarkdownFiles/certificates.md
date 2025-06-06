# Certificate Authority (CA)

openssl genrsa -out ca.key 2048

openssl req -new -key ca.key -subj "/CN=KUBERNETES-CA" -out ca.csr

openssl x509 -req -in ca.csr -signkey ca.key -out ca.crt

openssl genrsa -out admin.key 2048   # generate admin cert

openssl req -new -key ca.key -subj "/CN=kube-admin/O=system:masters" -out admin.csr 

openssl x509 -req -in admin.csr -CA ca.crt CAkey ca.key -out admin.crt


# ETCD

cat etcd.yaml

create the openssl.cnf


openssl req -new -key apiserver.key -subj "/CN=kube-apiserver" -out apiserver.csr -config openssl.cnf


openssl x509 -req -in apiserver.csr -CA ca.crt CAkey ca.key -out apiserver.crt

## View Certificate in clusters and add users

cat /etc/kubernetes/manifests/kube-apiserver.yaml  # kubeadm

cat /etc/system/systemd/kube-apiserver.yaml  # hard way

openssl x509 -in /etc/kubernetes/pki/apiserver.crt -text -noout

journalctl -u etcd.service -l 


kubectl logs etcd-master

docker ps -a 

docker logs 585474

crictl ps -a 

crictl logs containerID a28512290ffff


cat jane.csr | base64

kubectl get csr jane -o yaml
echo "ldgddy" | base64 --decode

kubectl certificate approve jane

kubectl certificate deny jane

kubectl delete csr agent-smith


# KubeCofig

curl https"//my-kube-playground:6443/api/v1/pods \
  --key admin.key
  --cert admin.crt
  --cacert ca.crt


kubectl get pods 
 --server my-kube-playground:6443
 --client-key admin.key
  --client-certificate admin.crt
  --certificate-authority ca.crt


kubectl get pods # $HOME/.kube/config
 --kubeconfig 


kubectl config view

kubectl config view --kubeconfig=my-custom-config

kubectl config use-context prod-user@production

kubectl config -h

kubectl config --kubeconfig=/root/my-kube-config use-context research

/* store the KUBe config as environment variable */

vi ~/.bashrc
export KUBECONFIG=/root/my-kube-config
source ~/.bashrc


# API GROUP

curl https://kube-master:6443/Version


curl https://kube-master:6443/api/v1/pods

curl https://kube-master:6443/api/v1/pods

curl http://localhost:6443 -k

curl http://localhost:6443/apis -k | grep "name" 

kubectl proxy 

curl http://localhost:8001 -k


# Role Base Access Controls (RBAC)

kubectl create -f devuser.yaml

kubectl get roles

kubectl get rolebindings

kubectl describe role developer

kubectl describe rolebinding dev-user-developer

kubectl auth can-i create deployments  # yes or no

kubectl auth can-i create deployments --as dev-user  --namespace test

# Cluster Roles and Role Bindings

kubectl api-resources --namespaced=false

kubectl api-resources --namespaced=false

kubectl get clusterroles



kubectl get clusterroles -o json | jq '.items | length'

kubectl get clusterrolebindings -o json | jq '.items | length'

kubectl create -f clusterroles.yaml 


# service Accounts
kubectl create serviceaccount dashboard-sa

kubectl get serviceaccount

kubectl describe serviceaccount dashboard-sa

kubectl describe  secret dashboard-sa-token-kbbm

kubectl exec -it my-kubernetes-dashboard -- ls /var/run/secrets/kubernetes.io/serviceaccount

kubectl create token dashboard-sa

kubectl set serviceaccount deploy/web-dashboard dashboard-sa

# cluster management

kube-controller-manager --pod-eviction-timeout=5m0s

kubectl drain node-1  # move pods to different nodes

kubectl uncordon node-1 # can make the node accesible to run pods again after draining

kubectl cordon node-2  # means the node cannot take pods till restriction is removed

kubectl drain node01 --ignore-daemonsets

# Upgrade clusters
sudo apt update
sudo apt-cache madison kubeadm

sudo apt-mark unhold kubeadm && \
sudo apt-get update && sudo apt-get install -y kubeadm='1.32.0' && \
sudo apt-mark hold kubeadm

apt-get upgrade -y kudeadm=1.12.0-00

sudo kubeadm upgrade apply 

kubeadm upgrade apply v1.12/0

kubectl get nofrd

apt-get upgrade -y kubelet=1.12.0-00

systemctl restart kubelet

kubectl drain node-1


kubeadm upgrade node config --kubelet-version v1.12.0

cat/etc/*release* # to see the release 


# upgrade control node and worker node 

kubectl drain controlplane --ignore-daemonsets

echo "deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.32/deb/ /" | sudo tee /etc/apt/sources.list.d/kubernetes.list

curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.32/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg


sudo apt-get update

sudo apt update
sudo apt-cache madison kubeadm

# replace x in 1.32.x-* with the latest patch version
sudo apt-mark unhold kubeadm && \
sudo apt-get update && sudo apt-get install -y kubeadm='1.32.0-*' && \
sudo apt-mark hold kubeadm

kubeadm version

sudo kubeadm upgrade plan

# replace x with the patch version you picked for this upgrade
sudo kubeadm upgrade apply v1.32.x

kubectl drain <node-to-drain> --ignore-daemonsets

# replace x in 1.32.x-* with the latest patch version
sudo apt-mark unhold kubelet kubectl && \
sudo apt-get update && sudo apt-get install -y kubelet='1.32.x-*' kubectl='1.32.x-*' && \
sudo apt-mark hold kubelet kubectl

sudo systemctl daemon-reload
sudo systemctl restart kubelet

# replace <node-to-uncordon> with the name of your node
kubectl uncordon <node-to-uncordon>

# drain the worker node

kubectl drain node01 --ignore-daemonsets

echo "deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.32/deb/ /" | sudo tee /etc/apt/sources.list.d/kubernetes.list

curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.32/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg


sudo apt-get update

sudo apt update
sudo apt-cache madison kubeadm

# replace x with the patch version you picked for this upgrade
sudo kubeadm upgrade node

kubectl drain <node-to-drain> --ignore-daemonsets

# replace x in 1.32.x-* with the latest patch version
sudo apt-mark unhold kubelet kubectl && \
sudo apt-get update && sudo apt-get install -y kubelet='1.32.0-*' kubectl='1.32.0-*' && \
sudo apt-mark hold kubelet kubectl

sudo systemctl daemon-reload
sudo systemctl restart kubelet

# replace <node-to-uncordon> with the name of your node
kubectl uncordon <node-to-uncordon>


# Backup - Resource COnfigs

kubectl get all -all-namespaces -o yaml > all-deploy-services.yaml

export ETCDCTL_API=3

etcdctl snapshot save -h

etcdctl snapshot restore -h

ETCDCTL_API=3 etcdctl \
   snapshot save snapshot.db

ls

ETCDCTL_API=3 etcdctl \
   snapshot status snapshot.db

service kube-apiserver stop

ETCDCTL_API=3 etcdctl \
   snapshot restore snapshot.db
   --data-dir /var/lib/etcd-from-backup

systemctl daemon-reload

service etcd restart

service kube-apiserver start

kubectl config get-clusters

kubectl config use-context cluster1

kubectl get nodes

kubectl config use-context cluster2

etcdctl \
   snapshot save --endpoint=  --cacert="" --cert="" --key="" /opt/cluster1.dbsnapshot.db

kubectl -n kube-system describe pod etcd-cluster1-controlplane | grep data-dir

ETCDCTL_API=3 etcdctl \
  --endpoints=https://127.0.0.1:2379 \
  --cacert=/etc/etcd/pki/ca.pem \
  --cert=/etc/etcd/pki/etcd.pem \
  --key=/etc/etcd/pki/etcd-key.pem \
   member l
   
 kubectl describe  pods -n kube-system etcd-cluster1-controlplane  | grep pki
      --cert-file=/etc/kubernetes/pki/etcd/server.crt
      --key-file=/etc/kubernetes/pki/etcd/server.key
      --peer-cert-file=/etc/kubernetes/pki/etcd/peer.crt
      --peer-key-file=/etc/kubernetes/pki/etcd/peer.key
      --peer-trusted-ca-file=/etc/kubernetes/pki/etcd/ca.crt
      --trusted-ca-file=/etc/kubernetes/pki/etcd/ca.crt
      /etc/kubernetes/pki/etcd from etcd-certs (rw)

ETCDCTL_API=3 etcdctl --endpoints=https://192.168.57.15:2379 --cacert=/etc/kubernetes/pki/etcd/ca.crt --cert=/etc/kubernetes/pki/etcd/server.crt --key=/etc/kubernetes/pki/etcd/server.key snapshot save /opt/cluster1.db


scp cluster1-controlplane:/opt/cluster1.db /opt


### Restore file

 kubectl config use-context cluster2

 scp /opt/cluster2.db etcd-server:/root

 ps -ef | grep -i etcd

  ETCDCTL_API=3 etcdctl --endpoints=https://127.0.0.1:2379 --cacert=/etc/etcd/pki/ca.pem --cert=/etc/etcd/pki/etcd.pem --key=/etc/etcd/pki/etcd-key.pem snapshot restore /root/cluster2.db --data-dir /var/lib/etcd-data-new
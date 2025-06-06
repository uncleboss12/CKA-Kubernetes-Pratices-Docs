# Linux Networking basics

ip link


ip addr add <ip-address> dev eth0

route

ip route add 192.168.2.0/24 via 192.168.2.1

ip add default via 192.168.2.1

cat /proc/sys/net/ipv4/ip_forward

ip netns add red

ip netns

ip link exec red ip link

ip -n red link

arp

ip netns exec red arp

ip netns exec red route

ip link add veth-red type veth peer name veth-blue

ip link set veth-red netns red

ip -n red addr add 192.168.15.1 dev veth-red

ip link add v-net-0 type bridge

ip link

ip link set dev v-net-0 up

ip -n del veth-red

# DNS configuration 

cat >> /etc/hosts
  192.168.1.11  db

cat >> /etc/resolv.conf
nameserver 192.168.1.100

cat /etc/nsswitch.conf

nslookup google.com


dig google.com
 
iptables -t nat -A POSTROUTING -s 192.168.15.0/24 -j MASQUERADE 

ip -n red addr add 192.168.1.10/24 dev veth-red

# Docker Networking

docker run --network none nginx

docker run --network none nginx

docker run --network host nginx

docker run nginx   # bridge

docker network ls

ip link 

ip netns

ip addr

docker inspect 223345rffbgdhed

ip -n bwhshdgbdvd  addr 

docker run -p 8080:80 nginx

iptables -nvL -t nat


# CNI

bridge add 2wehdbd  /var/run/netns/2wehdbd 


# Pod Network
ip link add v-net-0 type bridge

ip link set dev v-net-0 up

ip addr add 192.168.15/24 dev v-net-0

ip link add veth-red type veth peer name veth-red-br

ip link set veth-red netns red

ip -n red addr add 192.168.15.1 dev veth-red

ip -n red link set veth-red up

ip link set veth-red-br master v-net-0

ip netns exec blue ip route add 192.168.1.0/24 via 192.168.15.5

iptables -t nat -A POSTROUTING -s 192.168.15.0/24 -j MASQUERADE

```bash
ip lin


```bash
#!bin/bash
#Name: net-bash.sh
# CNI standards
ADD )
ip link add ....

# Attach veth pair
ip link set 

# Assign IP address
ip -n <namespace> route add ......

# Bring up Interface
ip -n <namespace> link set .....

# connect nodes to node
ip route add 10.244.2.2 via 192.168.1.0

DEL)
# DELETE VETH PAIR
ip link del
```

# CNI
# plugins configured in the path /etc/cni/nrt.d/bridge.conflist or flannel.conflist

ls /opt/cni/bin

ls /etc/cni/net.d

kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"

kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml

## WeaveWorks 

ps -aux | grep kubelet | grep --color container-runtime-endpoint

ls /opt/cni/bin

ls /opt/cni/bin/bridge

# Ip Management

weave allocate 10.32.0.0/12 for the entire network

range from 10.32.0.1 to 10.47.255.254


# Service Networking

kube-api-server --service-ip-range ipNet 

ps aux | grep kube-api-server

iptables -L -t nat | grep db-service

cat /var/log/kube-proxy.log

cat /etc/kubernetes/manifests/kube-apiserver.yaml   | grep cluster-ip-range


# DNS 

curl http://web-service.apps.svc.cluster.local  # for services

curl http://10-244-2-5.apps.pod.cluster.local  # for services


# CoreDNS

cat /etc/coredns/corefile

kubectl get configmap -n kube-system

cat /etc/resolv.conf

host ser-service

host 10-244-2-5.default.pod.cluster.local

kubectl exec -it hr -- nslookup mysql.payroll > /root/CKA/nslookup.out

# Ingress

kubectl create ingress ingress-test --rule="wear.my-online-store.com/wear*=wear-service:80"

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.12.2/deploy/static/provider/cloud/deploy.yaml


# Gateway API

kubectl kustomize "https://github.com/nginx/nginx-gateway-fabric/config/crd/gateway-api/standard?ref=v1.5.1" | kubectl apply -f -

kubectl apply -f https://raw.githubusercontent.com/nginx/nginx-gateway-fabric/v1.6.1/deploy/crds.yaml

kubectl apply -f https://raw.githubusercontent.com/nginx/nginx-gateway-fabric/v1.6.1/deploy/nodeport/deploy.yaml


kubectl get pods -n nginx-gateway

kubectl get svc -n nginx-gateway nginx-gateway -o yaml

kubectl patch svc nginx-gateway -n nginx-gateway --type='json' -p='[
  {"op": "replace", "path": "/spec/ports/0/nodePort", "value": 30080},
  {"op": "replace", "path": "/spec/ports/1/nodePort", "value": 30081}
]'


kubectl get gateways -n nginx-gateway


# Weave Net

kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml

# Flannel

kubectl apply -f https://raw.githubusercontent.com/coreos/flannel/2140ac876ef134e0ed5af15c65e414cf26827915/Documentation/kube-flannel.yml

# Calico

curl https://raw.githubusercontent.com/projectcalico/calico/v3.25.0/manifests/calico.yaml -O


# Troubleshooting Network Issues

proxy . /etc/resolv.conf



kubectl -n kube-system get deployment coredns -o yaml | \
  sed 's/allowPrivilegeEscalation: false/allowPrivilegeEscalation: true/g' | \
  kubectl apply -f -


https://kubernetes.io/docs/tasks/debug-application-cluster/debug-service/

https://kubernetes.io/docs/tasks/administer-cluster/dns-debugging-resolution/
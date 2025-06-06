# sysctl params required by setup, params persist across reboots
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.ipv4.ip_forward = 1
EOF

# Apply sysctl params without reboot
sudo sysctl --system

sudo modprobe br_netfilter

lsmod | grep br_netfilter

sudo sysctl net.bridge.bridge-nf-call-iptables=1
sudo sysctl net.bridge.bridge-nf-call-ip6tables=1

sudo sysctl -p

' go to the Documentations and follow the process of getting certificates and conf then install`

# for all nodes
sudo apt-get update
sudo apt-get install -y kubelet kubeadm=1.32.0-1.1 kubectl=1.32.0-1.1
sudo apt-mark hold kubelet kubeadm kubectl


sudo apt-get update 
sudo apt-get install -y containerd



ps -p 1

containerd config default | sed 's/SystemdCgroup = false/SystemdCgroup = true/' | sudo tee /etc/containerd/config.toml

cat /etc/containerd/config.toml | grep -i SystemdCgroup -B 50

sudo systemctl restart containerd

# control plane nodes

sudo kubeadm init --apiserver-advertise-address 10.0.0.6 --pod-network-cidr "10.244.0.0/16" --upload-certs  # for the control-plane nodes alone

sudo cat /etc/kubernetes/admin.conf

mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

kubectl apply -f https://github.com/flannel-io/flannel/releases/latest/download/kube-flannel.yml

# for the others worker nodes
 
kubeadm join 10.0.0.6:6443 --token mlazxg.uti87iro3dxqzzuz \
        --discovery-token-ca-cert-hash sha256:76355c8f4f76d942d19e416c3d41cdfa2e369acd6922305d5b4dd57835252982



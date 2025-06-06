# HPA Object creation to deployment

apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: webapp-hpa
  namespace: default
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: kkapp-deploy
    namespace: backend
  minReplicas: 1
  maxReplicas: 4
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 50
  behavior:
    scaleDown:
      stabilizationWindowSeconds: 30

# Update kubeadm cluster


# Enable IP forwarding
echo "net.ipv4.ip_forward = 1" >> /etc/sysctl.conf
echo "net.bridge.bridge-nf-call-iptables = 1" >> /etc/sysctl.conf

sysctl -p

sysctl -w net.ipv4.ip_forward=1
sysctl -w net.bridge.bridge-nf-call-iptables=1

sysctl -p

# move node storage capacity to file 
kubectl top nodes
kubectl top pods

kubectl get events --sort-by='.metadata.creationTimestamp'


# Install CNI cri-docker or 
sudo systemctl daemon-reload
sudo systemctl restart kubelet


# cluster role binding

apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: cluster-admin-binding-sa
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin # The ClusterRole to bind
subjects:
- kind: ServiceAccount
  name: my-service-account # Replace with your ServiceAccount name
  namespace: default       # Replace with the namespace of your ServiceAccount


# creating Netpol

apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-np-test-service
  namespace: default
spec:
  podSelector:
    matchLabels:
      app: np-test-service # Match the labels used by the service's selector
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector: {} # Allow traffic from all pods (adjust as needed)
    ports:
    - protocol: TCP
      port: 80


#  creating priorityclass
apiVersion: v1
kind: Pod
metadata:
  name: lp-pod
  namespace: low-priority
spec:
  priorityClassName: low-priority-class # Replace with your PriorityClass name
  containers:
  - name: example-container
    image: nginx 

apiVersion: scheduling.k8s.io/v1
kind: PriorityClass
metadata:
  name: low-priority-class
value: 50000
globalDefault: false
description: "Priority class for low-priority workloads"


# Creating PersistentVolume

apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-analytics
spec:
  capacity:
    storage: 100Mi
  volumeMode: Filesystem
  accessModes:
    - ReadWriteMany
  persistentVolumeReclaimPolicy: Recycle
  hostPath: # Corrected field
    path: /pv/data-analytics


# Gateway Creation

apiVersion: gateway.networking.k8s.io/v1beta1
kind: Gateway
metadata:
  name: web-gateway
  namespace: cka5673
spec:
  gatewayClassName: kodekloud
  listeners:
  - name: https
    protocol: HTTPS
    port: 443
    hostname: example.com # Replace with your desired hostname
    tls:
      mode: Terminate
      certificateRefs:
      - kind: Secret
        name: kodekloud-tls
    allowedRoutes:
      namespaces:
        from: All


# Resources mahanement in Nodes and Pods

resources:
  requests:
    cpu: "50m"   # Reduced from 100m to 50m
    memory: "90Mi"   # Reduced from 128Mi to 90Mi (Fits within quota)
  limits:
    cpu: "150m"   
    memory: "150Mi"

kubectl get pods -n default

kubectl get rs -n default

kubectl delete rs backend-api-7977bfdbd5 -n default

kubectl get pods -n default


# taint nodes
kubectl taint node node01 env_type=production:NoSchedule

kubectl run dev-redis --image=redis:alpine

kubectl get pods -o wide

---
apiVersion: v1
kind: Pod
metadata:
  name: prod-redis
spec:
  containers:
  - name: prod-redis
    image: redis:alpine
  tolerations:
  - effect: NoSchedule
    key: env_type
    operator: Equal
    value: production


# sidecar containers

apiVersion: v1
kind: Pod
metadata:
  name: mc-pod
  namespace: mc-namespace
spec:
  containers:
    - name: mc-pod-1
      image: nginx:1-alpine
      env:
        - name: NODE_NAME
          valueFrom:
            fieldRef:
              fieldPath: spec.nodeName
    - name: mc-pod-2
      image: busybox:1
      volumeMounts:
        - name: shared-volume
          mountPath: /var/log/shared
      command:
        - "sh"
        - "-c"
        - "while true; do date >> /var/log/shared/date.log; sleep 1; done"
    - name: mc-pod-3
      image: busybox:1
      command:
        - "sh"
        - "-c"
        - "tail -f /var/log/shared/date.log"
      volumeMounts:
        - name: shared-volume
          mountPath: /var/log/shared
  volumes:
    - name: shared-volume
      emptyDir: {}
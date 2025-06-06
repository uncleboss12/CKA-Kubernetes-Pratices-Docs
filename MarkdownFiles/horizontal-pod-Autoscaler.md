# scale pods imperatively
kubectl top pod my-app

kubectl scale deployment my-app --replicas=3

kubectl autoscale deployment my-app\
    --cpu-percent=50 --min=1 --max=10

kubectl get hpa

kubectl delete hpa my-app

## Declarive way to create Autoscaler

`create a yaml file with kind:HorizontalPodAutoscaler`


# Vertical Scaling VPA

kubectl apply -f 

kubectl get pods -n kube-system | grep vpa

kubectl describe vpa my-app-vpa

kubectl apply -f /root/vpa-crds.yml  # Install VPA Custom Resource Definitions (CRDs)

kubectl apply -f /root/vpa-rbac.yml Install VPA Role-Based Access Control (RBAC)

# Clone the VPA Repository and Set Up the Vertical Pod Autoscaler

git clone https://github.com/kubernetes/autoscaler.git 

cd autoscaler/vertical-pod-autoscaler

./hack/vpa-up.sh

kubectl apply -f flask-deployment.yml

kubectl scale deployment flask-app --replicas=2

kubectl get deployment flask-app -o wide

kubectl get pods -l app=flask-app

kubectl describe vpa flask-app

kubectl top pod # to display metrics of the pods

kubectl get vpa
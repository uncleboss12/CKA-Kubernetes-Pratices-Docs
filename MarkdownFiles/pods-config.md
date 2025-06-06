Kubectl run --image=nginx:1.7.9 --replicas=2 --port=80 --labels="app=nginx,env=prod" nginx-prod

kubectl run redis --image=redis123 --dry-run=client -o yaml > redis.yaml

kubectl get pods 

kubectl get pods -l app=nginx

kubectl describe pods nginx-prod-7b4c8b5c6f-7z5zr

kubectl apply -f pods-config.yml

kubectl delete pods nginx-prod-7b4c8b5c6f-7z5zr


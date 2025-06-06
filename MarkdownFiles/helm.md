# Helm package manager

helm install wordpress

helm upgrade wordpress

helm rollback wordpress

helm uninstall wordpress


# installing Helm

helm search wordpress

helm search hub wordpress

helm repo add bitnami "https://"

helm install my-release bitnami/wordpress

helm list

helm uninstall my-release

helm repo

helm repo list

helm repo update

helm install --set wordpressBlogName="Helm Tutorials" my-release bitnami/wordpress

helm install --values custom-values.yaml my-release bitnami/wordpress

helm pull bitnami/wordpress

helm pull --untar  bitnami/wordpress

helm install my-release ./wordpress

helm search repo wordpress

helm repo remove hashicorp

# Helm Lifecycle Management

helm install nginx-release bitnami/nginx --version 7.1.0

helm upgrade nginx-release bitnami/nginx

helm list

helm history nginx-release

helm rollback nginx-relese 1

## N.B 

helm repo update
helm search repo nginx 
helm upgrade kk-mock1 kk-mock1/nginx --version 18.1.15
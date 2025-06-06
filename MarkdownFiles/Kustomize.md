kustomize build k8s/  # this is for dry-run

kustomize build k8s/ | kubectl apply -f -  # this is to apply changes

kubectl apply -k k8s/


kustomize build k8s/ | kubectl delete -f -  # this is to delete resources 

kubectl delete -k k8s/

# install Kustomize

curl -s "https://raw.githubusercontent.com/kubernetes-sigs/kustomize/master/hack/install_kustomize.sh"  | bash

kustomize version 
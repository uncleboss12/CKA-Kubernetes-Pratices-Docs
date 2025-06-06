# docker storage 
/var/lib/docker
- aufs
- containers
- image
- volumes


docker volume create data_volume

docker run -v data_volume:/var/lib/mysql mysql  # data volume in docker volume

docker run -v /data/mysql:/var/lib/mysql mysql  # external data folder

docker run --mount type=bind, source=d/data/mysql, target=/var/lib/mysql mysql


docker run -it \
  --name mysql
  --volume-driver rexray/ebs \
  --mount src=ebs-vol,target=/var/lib/mysql \
  mysql


# Container Storage Interface (CSI)
Portworx, amazon EBS, GlusterFS, Dell EMC

## Container Network Interface
 weaveworks, flannel, cilium

## Container Resource Interface
 rkt, docker, cri-o


# Volumes

kubectl get persistentvolume 

kubectl get persistentvolumeclaim

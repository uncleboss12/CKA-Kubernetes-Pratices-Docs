---
apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
metadata:
  name: john-developer
spec:
  signerName: kubernetes.io/kube-apiserver-client
  request: LS0tLS1CRUdJTiBDRVJUSUZJQ0FURSBSRVFVRVNULS0tLS0KTUlJQ1ZEQ0NBVHdDQVFBd0R6RU5NQXNHQTFVRUF3d0VhbTlvYmpDQ0FTSXdEUVlKS29aSWh2Y05BUUVCQlFBRApnZ0VQQURDQ0FRb0NnZ0VCQUt2Um1tQ0h2ZjBrTHNldlF3aWVKSzcrVVdRck04ZGtkdzkyYUJTdG1uUVNhMGFPCjV3c3cwbVZyNkNjcEJFRmVreHk5NUVydkgyTHhqQTNiSHVsTVVub2ZkUU9rbjYra1NNY2o3TzdWYlBld2k2OEIKa3JoM2prRFNuZGFvV1NPWXBKOFg1WUZ5c2ZvNUpxby82YU92czFGcEc3bm5SMG1JYWpySTlNVVFEdTVncGw4bgpjakY0TG4vQ3NEb3o3QXNadEgwcVpwc0dXYVpURTBKOWNrQmswZWhiV2tMeDJUK3pEYzlmaDVIMjZsSE4zbHM4CktiSlRuSnY3WDFsNndCeTN5WUFUSXRNclpUR28wZ2c1QS9uREZ4SXdHcXNlMTdLZDRaa1k3RDJIZ3R4UytkMEMKMTNBeHNVdzQyWVZ6ZzhkYXJzVGRMZzcxQ2NaanRxdS9YSmlyQmxVQ0F3RUFBYUFBTUEwR0NTcUdTSWIzRFFFQgpDd1VBQTRJQkFRQ1VKTnNMelBKczB2czlGTTVpUzJ0akMyaVYvdXptcmwxTGNUTStsbXpSODNsS09uL0NoMTZlClNLNHplRlFtbGF0c0hCOGZBU2ZhQnRaOUJ2UnVlMUZnbHk1b2VuTk5LaW9FMnc3TUx1a0oyODBWRWFxUjN2SSsKNzRiNnduNkhYclJsYVhaM25VMTFQVTlsT3RBSGxQeDNYVWpCVk5QaGhlUlBmR3p3TTRselZuQW5mNm96bEtxSgpvT3RORStlZ2FYWDdvc3BvZmdWZWVqc25Yd0RjZ05pSFFTbDgzSkljUCtjOVBHMDJtNyt0NmpJU3VoRllTVjZtCmlqblNucHBKZWhFUGxPMkFNcmJzU0VpaFB1N294Wm9iZDFtdWF4bWtVa0NoSzZLeGV0RjVEdWhRMi80NEMvSDIKOWk1bnpMMlRST3RndGRJZjAveUF5N05COHlOY3FPR0QKLS0tLS1FTkQgQ0VSVElGSUNBVEUgUkVRVUVTVC0tLS0tCg==
  usages:
  - digital signature
  - key encipherment
  - client auth


aapiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
metadata:
  name: john-developer
spec:
  signerName: kubernetes.io/kube-apiserver-client
  request: |
    MIICVDCCATwCAQAwDzENMAsGA1UEAwwEam9objCCASIwDQYJKoZIhvcNAQEBBQAD
    ggEPADCCAQoCggEBAOgRyPHAkkA/do6oBkn4LIPyrudnMadN5Z2OW7XypJDQi8fm
    dU5SjrKokFA633oJ97XXXhQPHtYfkK1s4F9D91VpLL2AAmpFII0HNydzzxPM7ovM
    YruB8jheCc/4eUgPrAe60M2xCZd6Qjk8E0s7YriIBifUe1yEiJcGlzuBklpF4mfO
    vKbdEGXGcssZLRey1m4VWqcD65UyBQrkibKKh5wSYIl5CjXpgJQiGJVNasPg4V5Z
    QkEsmys4Avo20r6mi8rAXGEK/DRsjH9JcnmFG5qgUKqdy5gfyqs8FOGBZbleewUB
    3WLWOVfuscBW93kWs/lcD92pqYSe6FiAeR5hlXsCAwEAAaAAMA0GCSqGSIb3DQEB
    CwUAA4IBAQBa6oAIEzyST+6XmDltUnLd6EqFevvUoUS4n4b+57Oosv006avFXvbM
    n1RojyK20uOVIwSqxdUQheGLF5oX27ckNPXgPUrKslRn6DNDD76KohNhMH6I2hIQ
    wIZgzm/Zl4ZWDH3AUQdY47PpIeTDhiwWjolfao2x+OFn2cBjVGwnt56wmZrNhMk+
    TyDqbjWWYO3jBdCOXfNoZtEzou9FA9ojZBp4Eg2pqfPPvhoRfkFwwPCi/y7KJ51T
    MjiFLyOpa3e31LFnaw/CILykQUwU9CdEawYhPsrjobjovBJB2JfpGpGxq5BL6eMy
    PmWfHnSAw0g1r1x8JrEfVGhc6DXxM9Ve
  usages:
    - digital signature
    - key encipherment
    - client auth

kubectl certificate approve john-developer
kubectl create role developer --resource=pods --verb=create,list,get,update,delete --namespace=development

kubectl create rolebinding developer-role-binding --role=developer --user=john --namespace=development


kubectl auth can-i update pods --as=john --namespace=development


kubectl run nginx-resolver --image=nginx
kubectl expose pod nginx-resolver --name=nginx-resolver-service --port=80 --target-port=80 --type=ClusterIP

kubectl run test-nslookup --image=busybox:1.28 --rm -it --restart=Never -- nslookup nginx-resolver-service
kubectl run test-nslookup --image=busybox:1.28 --rm -it --restart=Never -- nslookup nginx-resolver-service > /root/CKA/nginx.svc

kubectl get pod nginx-resolver -o wide
kubectl run test-nslookup --image=busybox:1.28 --rm -it --restart=Never -- nslookup <P-O-D-I-P.default.pod> > /root/CKA/nginx.pod


kubectl run nginx-critical --image=nginx --dry-run=client -o yaml > static.yaml

root@cluster1-controlplane:~# scp static.yaml cluster1-node01:/root/

root@cluster1-controlplane:~# kubectl get nodes -o wide

# Perform SSH
root@cluster1-controlplane:~# ssh cluster1-node01
OR
root@cluster1-controlplane:~# ssh <IP of cluster1-node01>

root@cluster1-node01:~# mkdir -p /etc/kubernetes/manifests

root@cluster1-node01:~# vi /var/lib/kubelet/config.yaml

root@cluster1-node01:~# cp /root/static.yaml /etc/kubernetes/manifests/


journalctl -xe

systemctl status kubelet

sudo systemctl start kubelet

sudo systemctl enable kubelet

kubectl get nodes



helm ls -A

kubectl get deploy -n <NAMESPACE> <DEPLOYMENT-NAME> -o json | jq -r '.spec.template.spec.containers[].image'


helm uninstall <RELEASE-NAME> -n <NAMESPACE>

kubectl apply -f /root/net-pol-3.yaml

kubectl get netpol -n backend


kubectl edit deployment backend-api -n default

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



kubectl create -f https://raw.githubusercontent.com/projectcalico/calico/v3.29.2/manifests/tigera-operator.yaml

curl https://raw.githubusercontent.com/projectcalico/calico/v3.29.2/manifests/custom-resources.yaml -O

kubectl create -f custom-resources.yaml

watch kubectl get pods -n calico-system

kubectl run web-app --image nginx

kubectl get pod web-app -o jsonpath='{.status.podIP}'

kubectl run test --rm -it -n kube-public --image=jrecord/nettools --restart=Never -- curl <IP>


# logger-deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: logging-deployment
  namespace: logging-ns
spec:
  replicas: 1
  selector:
    matchLabels:
      app: logger
  template:
    metadata:
      labels:
        app: logger
    spec:
      volumes:
      - name: log-volume
        emptyDir: {}
      containers:
      - name: app-container
        image: busybox
        command:
        - sh
        - -c
        - "while true; do echo 'Log entry' >> /var/log/app/app.log; sleep 5; done"
        volumeMounts:
        - name: log-volume
          mountPath: /var/log/app
      - name: log-agent
        image: busybox
        command:
        - tail
        - -f
        - /var/log/app/app.log
        volumeMounts:
        - name: log-volume
          mountPath: /var/log/app

 

apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: webapp-ingress
  annotations:
    nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  ingressClassName: nginx
  rules:
  - host: kodekloud-ingress.app
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: webapp-svc
            port:
              number: 80



apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: webapp-hpa
  namespace: backend
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: kkapp-deploy
  minReplicas: 3
  maxReplicas: 15
  metrics:
  - type: Resource
    resource:
      name: memory
      target:
        type: Utilization
        averageUtilization: 65
status:
  observedGeneration: 1
  lastScaleTime: <some-time>
  currentReplicas: 1
  desiredReplicas: 1
  currentMetrics:
  - type: Resource
    resource:
      name: memory
      current:
        averageUtilization: 0
        averageValue: 0


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
    tls:
      mode: Terminate
      certificateRefs:
      - kind: Secret
        name: kodekloud-tls 
    allowedRoutes:
      namespaces:
        from: All


kubectl get deploy -n atlanta-page-04 atlanta-page-apd -o json | jq -r '.spec.template.spec.containers[].image'


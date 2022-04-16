## 1-Create Kubernets On DigitalOcean.
## 2-Deploy application Web
### 2.1-Setting Up Hello World Deployments
```
nano hello-kubernetes-first.yaml 
```
```
kubectl create -f hello-kubernetes-first.yaml
kubectl get service hello-kubernetes-first
```

### 2.2-Installing the Kubernetes Nginx Ingress Controller
```
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
helm install nginx-ingress ingress-nginx/ingress-nginx --set controller.publishService.enabled=true
kubectl --namespace default get services -o wide -w nginx-ingress-ingress-nginx-controller
```

### 2.3-Exposing the App Using an Ingress
```
nano hello-kubernetes-ingress.yaml
```
```
kubectl apply -f hello-kubernetes-ingress.yaml
```
### 2.4-Securing the Ingress Using Cert-Manager
```
kubectl create namespace cert-manager
helm repo add jetstack https://charts.jetstack.io
helm repo update
helm install cert-manager jetstack/cert-manager --namespace cert-manager --version v1.2.0 --set installCRDs=true
```
```
nano production_issuer.yaml
```
```
kubectl apply -f production_issuer.yaml
```
```
nano hello-kubernetes-ingress-ssl.yaml
```
```
kubectl apply -f hello-kubernetes-ingress.yaml
kubectl describe certificate hello-kubernetes-tls
```
---




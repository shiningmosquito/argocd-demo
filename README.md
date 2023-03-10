# A side project of practice ArgoCD
## Installation 
### 1. Create namespace for ArgoCD:
```
kubectl create namespace argocd
```
### 2. Install ArgoCD controller:
```
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```
### 3. Check ArgoCD readiness:
```
kubectl -n argocd get pods

NAME                                                READY   STATUS    RESTARTS   AGE
argocd-application-controller-0                     1/1     Running   0          61m
argocd-applicationset-controller-75598f7f9d-l7dzk   1/1     Running   0          61m
argocd-dex-server-7f954949fc-r2mhz                  1/1     Running   0          61m
argocd-notifications-controller-89f9c7c79-scgff     1/1     Running   0          61m
argocd-redis-547f5d94cd-mzxfd                       1/1     Running   0          61m
argocd-repo-server-6f85cf755d-db8zk                 1/1     Running   0          61m
argocd-server-bf6b8fbfd-gdccw                       1/1     Running   0          61m
```
### 4. Access ArgoCD UI:
```
kubectl port-forward svc/argocd-server -n argocd 8080:443

Forwarding from 127.0.0.1:8080 -> 8080
Forwarding from [::1]:8080 -> 8080
```
### 5. Get default password of ArgoCD UI:
Default username is `admin`
```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo

6DZk03C-vNZ7GKZX
```
### 6. Modify password of ArgoCD UI (optional):
#### 6.1 Login to Argo CD via Argo CD CLI:
```
argocd login localhost:8080 - username admin - password 6DZk03C-vNZ7GKZX - insecure
'admin:login' logged in successfully
Context 'localhost:8080' updated
```
#### 6.2 Update default admin password via Arog CD CLI:
```
argocd account update-password --account admin --current-password 6DZk03C-vNZ7GKZX --new-password xxxx
```

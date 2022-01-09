# argocd-mj

How to quickly get up and running K8 cluster with Argo CD 

## Steps to reproduce:

1. Install k3d, helm and kubectl

2. Checkout the repo 

3. Create cluster
```
  k3d cluster create --config dev-cluster.k3d.yaml
```

4. Create argocd namespace
```
  kubectl create ns argocd 
  helm install argo-cd charts/argo-cd/ -n argocd
```  

5. Install root application
```
helm template apps/ | kubectl apply -n argocd -f -
```
  
## Some commands for quick reference
Initial password for ArgoCD version v2.2.

```
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```

Port forwarding 
```
kubectl -n argocd port-forward svc/argo-cd-argocd-server 8080:443
```

---
*Based on the* https://www.arthurkoziel.com/setting-up-argocd-with-helm/

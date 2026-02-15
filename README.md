# argo-cd_howto
Argo-CD HowTo Doc

Demo repo: https://github.com/sidd-harth/gitops-argocd


## Install
```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/v2.14.9/manifests/install.yaml

# convert to NodePort
k -n argocd edit svc argocd-server
# admin password
k -n argocd get secrets argocd-initial-admin-secret -o json | jq .data.password -r | base64 -d


wget https://github.com/argoproj/argo-cd/releases/download/v2.14.9/argocd-linux-amd64
mv argocd-linux-amd64 argocd
chmod +x argocd 
mv argocd /usr/bin/
```

## Create Application

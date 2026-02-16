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

## Create Application and Projects

```bash
argocd app list
k -n argo-cd get app
k -n argo-cd get appproj

argocd app create solar-system-app-2 --repo https://3000-port-4sfx47qep53aadt5.labs.kodekloud.com/bob/gitops-argocd.git \
--dest-server https://kubernetes.default.svc \
--path ./solar-system --dest-name space solar-system

argocd app sync solar-system-app-2
``` 

## Reconciliation Loops

```bash
kubectl -n argocd patch configmap argocd-cm --patch='{"data":{"timeout.reconciliation":"300s"}}'
k -n argocd rollout restart deployment argocd-repo-server
k -n argocd get cm argocd-cm -o yaml
```

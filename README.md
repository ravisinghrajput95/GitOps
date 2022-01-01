# Simple GitOps flow using Github actions and ArgoCD for deployment on GKE.

Install argo-cd in GKE cluster:
#create new namespace
kubectl create namespace argocd
#running the deployment
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

#Patch the argocd-server with service type as LoadBalancer
kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'
#Retrieve the initial password for ArgoCD login
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d

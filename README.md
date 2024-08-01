## Argocd installation on killerkoda lab

git clone https://github.com/anirudhadak2/kucl2022.git

ls

cd kucl2022  

ls

kubectl create ns argocd 

kubectl get ns

kubectl create  -n argocd  -f install.yaml

ls

kubectl get pod

kubectl get pod -n argocd

kubectl get svc -n argocd

kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo

##   get password for login into the agrocd gui account  Username : admin 


==========================================================================================
## Another Way to Install Argocd on K8s Cluster

Step 1. →Install Argo cd

Argo CD is a tool that helps software developers and teams manage and deploy their applications to Kubernetes clusters more easily. 
It simplifies the process of keeping your applications up to date and in sync with your desired configuration by automatically syncing 
your code with what’s running in your Kubernetes environment.
 It’s like a traffic cop for your chmod 700 get_helm.shapplications on Kubernetes, ensuring they are always in the right state without 
you having to manually make changes.


1. Add the Argo CD Helm repository:
helm repo add argo-cd https://argoproj.github.io/argo-helm

2. Update your Helm repositories:
helm repo update

3. Create a namespace for Argo CD (optional but recommended):
kubectl create namespace argocd


4. Install Argo CD using Helm:
helm install argocd argo-cd/argo-cd -n argocd


5. kubectl get all -n argocd


====================
Expose argocd-server
By default argocd-server is not publicaly exposed. For the purpose of this workshop, we will use a Load Balancer to make it usable:

kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "LoadBalancer"}}'

export ARGOCD_SERVER=`kubectl get svc argocd-server -n argocd -o json | jq — raw-output ‘.status.loadBalancer.ingress[0].hostname’`

echo $ARGOCD_SERVER


============================
you have given a url copy and paste it on your chrome browser


For Password →

export ARGO_PWD=`kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath=”{.data.password}” | base64 -d`

echo $ARGO_PWD

output == password for argocd

==================================



Step 2 →Deploy Application with ArgoCD
Sign into argo cd using above steps →



1.  go to setting →repositories →connect repo

2. click on connect output →successful

3. Now go to application →newapp


4. select the above options and click on create

5. Now click on sync →force →sync →ok


6.go to your cluster and select the node created by node group and expose port 30007


=============================================================================================================




   

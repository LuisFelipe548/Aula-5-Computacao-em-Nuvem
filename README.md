Codigo Passo:2

kubectl version --client
Client Version: v1.37.1
Kustomize Version: v5.8.1
root@controlplane:~$ kubectl get nodes
NAME           STATUS   ROLES           AGE   VERSION
controlplane   Ready    control-plane   9d    v1.37.1
node01         Ready    <none>          9d    v1.37.1

Codigo Passo:3 
kubectl create deployment web-aula5 --image=nginx:alpine
deployment.apps/web-aula5 created
root@controlplane:~$ kubectl get deployments
NAME        READY   UP-TO-DATE   AVAILABLE   AGE
web-aula5   1/1     1            1           18s
root@controlplane:~$ kubectl get pods
NAME                         READY   STATUS    RESTARTS   AGE
web-aula5-779c6f9566-sjss9   1/1     Running   0          2m18s

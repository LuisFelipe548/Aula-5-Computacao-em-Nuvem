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

Codigo Passo:4 

 kubectl get pods
NAME                         READY   STATUS    RESTARTS   AGE
web-aula5-779c6f9566-sjss9   1/1     Running   0          2m18s
root@controlplane:~$ kubectl get pods -o wide
NAME                         READY   STATUS    RESTARTS   AGE     IP              NODE     NOMINATED NODE   READINESS GATES
web-aula5-779c6f9566-sjss9   1/1     Running   0          2m40s   192.168.1.178   node01   <none>           <none>


Codigo Passo:5 

 kubectl describe pod $(kubectl get pods -o  jsonpath='{.items[0].metadata.name}')
Name:             web-aula5-779c6f9566-sjss9
Namespace:        default
Priority:         0
Service Account:  default
Node:             node01/172.30.2.2
Start Time:       Wed, 14 Oct 2026 23:29:32 +0000
Labels:           app=web-aula5
                  pod-template-hash=779c6f9566
Annotations:      <none>
Status:           Running
IP:               192.168.1.178
IPs:
  IP:           192.168.1.178
Controlled By:  ReplicaSet/web-aula5-779c6f9566
Containers:
  nginx:
    Container ID:   containerd://99d2be148492e09cc5501d41e268cae411778047c707f1494a0087162922988a
    Image:          nginx:alpine
    Image ID:       docker.io/library/nginx@sha256:0e5caf3555a79db2f1624c61fb1e585c4298a26384fea83f3e5108e451c1eb2c
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Wed, 14 Oct 2026 23:29:39 +0000
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-h74tc (ro)
Conditions:
  Type                        Status
  PodReadyToStartContainers   True 
  Initialized                 True 
  Ready                       True 
  ContainersReady             True 
  PodScheduled                True 
Volumes:
  kube-api-access-h74tc:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    Optional:                false
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age   From               Message
  ----    ------     ----  ----               -------
  Normal  Scheduled  5m7s  default-scheduler  Successfully assigned default/web-aula5-779c6f9566-sjss9 to node01
  Normal  Pulling    5m3s  kubelet            spec.containers{nginx}: Pulling image "nginx:alpine"
  Normal  Pulled     5m    kubelet            spec.containers{nginx}: Successfully pulled image "nginx:alpine" in 3.145s (3.145s including waiting). Image size: 28826677 bytes.
  Normal  Created    5m    kubelet            spec.containers{nginx}: Container created
  Normal  Started    5m    kubelet            spec.containers{nginx}: Container started

Codigo Passo:6 

 kubectl scale deployment web-aula5 --replicas=3
deployment.apps/web-aula5 scaled
root@controlplane:~$ kubectl get pods -o wide
NAME                         READY   STATUS    RESTARTS   AGE     IP              NODE     NOMINATED NODE   READINESS GATES
web-aula5-779c6f9566-64v8h   1/1     Running   0          27s     192.168.1.28    node01   <none>           <none>
web-aula5-779c6f9566-9dm9q   1/1     Running   0          27s     192.168.1.171   node01   <none>           <none>
web-aula5-779c6f9566-sjss9   1/1     Running   0          6m42s   192.168.1.178   node01   <none>           <none>

Codigo Passo:7 

kubectl get deployment,replicaset,pods
NAME                        READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/web-aula5   3/3     3            3           8m8s

NAME                                   DESIRED   CURRENT   READY   AGE
replicaset.apps/web-aula5-779c6f9566   3         3         3       8m8s

NAME                             READY   STATUS    RESTARTS   AGE
pod/web-aula5-779c6f9566-64v8h   1/1     Running   0          112s
pod/web-aula5-779c6f9566-9dm9q   1/1     Running   0          112s
pod/web-aula5-779c6f9566-sjss9   1/1     Running   0          8m7s


Codigo Passo:8 

kubectl delete pod $(kubectl get pods -o jsonpath='{.items[0].metadata.name}')
pod "web-aula5-779c6f9566-64v8h" deleted from default namespace
root@controlplane:~$ kubectl get pods
NAME                         READY   STATUS    RESTARTS   AGE
web-aula5-779c6f9566-9dm9q   1/1     Running   0          5m20s
web-aula5-779c6f9566-9q7zs   1/1     Running   0          12s
web-aula5-779c6f9566-sjss9   1/1     Running   0          11m


Codigo Passo:9 

NAME          TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)   AGE
web-service   ClusterIP   10.96.123.456   <none>        80/TCP    10s

Codigo Passo:10 

<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
...
</html>
pod "teste" deleted

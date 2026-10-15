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




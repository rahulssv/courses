# Kubernetes Day 5

`ubuntu@ubuntu-VM:~$ kubectl get ns`

```{r}
NAME                   STATUS   AGE
default                Active   224d
kube-node-lease        Active   224d
kube-public            Active   224d
kube-system            Active   224d
kubernetes-dashboard   Active   3d
novgems                Active   5d
test                   Active   6d
```

`ubuntu@ubuntu-VM:~$ kubectl get pods - test`

```{r}
Error from server (NotFound): pods "-" not found
Error from server (NotFound): pods "test" not found
```

`ubuntu@ubuntu-VM:~$ kubectl get pods -n test`

```{r}
No resources found in test namespace.
```

`ubuntu@ubuntu-VM:~$ kubectl svc -n test`

```{r}
error: unknown command "svc" for "kubectl"
Did you mean this?set
```

`ubuntu@ubuntu-VM:~$ kubectl get svc -n test`

```{r}
No resources found in test namespace.
```

`ubuntu@ubuntu-VM:~$ kubectl create ns training-2`

```{r}
namespace/training-2 created
```

`ubuntu@ubuntu-VM:~$ kubectl create deploy nginxcip --image=nginx -n training-2`

```{r}
deployment.apps/nginxcip created
```

`ubuntu@ubuntu-VM:~$ kubectl expose deploy nginxcip --port=80 -n  training-2`

```{r}
service/nginxcip exposed
```

`ubuntu@ubuntu-VM:~$ kubectl get service nginxcip  -n  training-2 --output yaml`

```{r}
apiVersion: v1
kind: Service
metadata:
  creationTimestamp: "2023-11-06T05:54:20Z"
  labels:
    app: nginxcip
  name: nginxcip
  namespace: training-2
  resourceVersion: "436296"
  uid: 544c3cf4-c62a-4930-a0a8-5de17027a78b
spec:
  clusterIP: 10.103.225.181
  clusterIPs:
  - 10.103.225.181
  internalTrafficPolicy: Cluster
  ipFamilies:
  - IPv4
  ipFamilyPolicy: SingleStack
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  selector:
    app: nginxcip
  sessionAffinity: None
  type: ClusterIP
status:
  loadBalancer: {}
```

`ubuntu@ubuntu-VM:~$ curl localhost:80`

```{r}
curl: (7) Failed to connect to localhost port 80 after 0 ms: Connect                                         ion refused
```

`ubuntu@ubuntu-VM:~$ Node port`

```{r}
Command 'Node' not found, did you mean:
  command 'code' from snap code (d037ac07)
  command 'ode' from deb plotutils (2.6-11)
  command 'node' from deb nodejs (12.22.9~dfsg-1ubuntu3.1)
See 'snap info <snapname>' for additional versions.

```

`ubuntu@ubuntu-VM:~$ kubectl get deployment  -n  training-2`

```{r}
NAME       READY   UP-TO-DATE   AVAILABLE   AGE
nginxcip   1/1     1            1           10m
```

`ubuntu@ubuntu-VM:~$ kubectl expose deploy nginx --port=80 --type=NodePort  -n  training-2`

```{r}
Error from server (NotFound): deployments.apps "nginx" not found
```

`ubuntu@ubuntu-VM:~$ kubectl expose deploy nginxcip --port=80 --type=NodePort  -n  training-2`

```{r}
Error from server (AlreadyExists): services "nginxcip" already exists
```

`ubuntu@ubuntu-VM:~$ kubectl get svc -n  training-2`

```{r}
NAME       TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)   AGE
nginxcip   ClusterIP   10.103.225.181   <none>        80/TCP    13m
```

`ubuntu@ubuntu-VM:~$ curl localhost:32066`

```{r}
curl: (7) Failed to connect to localhost port 32066 after 0 ms: Conn                                         ection refused
```

`ubuntu@ubuntu-VM:~$ curl localhost:80`

```{r}
curl: (7) Failed to connect to localhost port 80 after 0 ms: Connect                                         ion refused
```

`ubuntu@ubuntu-VM:~$ curl 10.103.225.181:80`

```{r}
curl: (7) Failed to connect to 10.103.225.181 port 80 after 2 ms: No                                          route to host
```

`ubuntu@ubuntu-VM:~$ kubectl get nodes --output wide`

```{r}
NAME       STATUS   ROLES                  AGE    VERSION    INTERNA                                         L-IP    EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION     CONTAI                                         NER-RUNTIME
minikube   Ready    control-plane,master   224d   v1.23.12   192.168                                         .49.2   <none>        Ubuntu 20.04.5 LTS   6.2.0-34-generic   docker                                         ://20.10.23
```

`ubuntu@ubuntu-VM:~$ curl localhost`

```{r}
curl: (7) Failed to connect to localhost port 80 after 0 ms: Connec                                          tion refused
```

`ubuntu@ubuntu-VM:~$ curl 192.16.49.2:80`

```{r}
<?xml version="1.0" encoding="iso-8859-1"?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
         "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
        <head>
                <title>404 - Not Found</title>
        </head>
        <body>
                <h1>404 - Not Found</h1>
        </body>
</html>
```

`ubuntu@ubuntu-VM:~$ kubectl get pods -o wide`

```{r}
NAME                                READY   STATUS             REST                                          ARTS       AGE    IP            NODE       NOMINATED NODE   READINE                                          SS GATES
hello-node-cdcf64657-9chvx          1/1     Running            0                                                        3d1h   172.17.0.9    minikube   <none>           <none>
my-dep-6d55d579d5-9xrx9             1/1     Running            2 (3                                          d1h ago)   4d     172.17.0.2    minikube   <none>           <none>
nginx-deployment-5b4685b9bd-hhrrr   0/1     ImagePullBackOff   0                                                        3d     172.17.0.11   minikube   <none>           <none>
nginx-deployment-ff6655784-4dk7k    1/1     Running            0                                                        3d     172.17.0.10   minikube   <none>           <none>
nginx-deployment-ff6655784-thfjl    1/1     Running            0                                                        3d     172.17.0.12   minikube   <none>           <none>
nginx-deployment-ff6655784-zg86c    1/1     Running            0                                                        3d     172.17.0.13   minikube   <none>           <none>
pod1                                1/1     Running            2 (3                                          d1h ago)   4d     172.17.0.4    minikube   <none>           <none>
pod2                                1/1     Running            2 (3                                          d1h ago)   4d     172.17.0.5    minikube   <none>           <none>
```

`ubuntu@ubuntu-VM:~$ kubectl get pods -o wide -n test-2`

```{r}
No resources found in test-2 namespace.
```

`ubuntu@ubuntu-VM:~$ kubectl get pods -o wide`

```{r}
NAME                                READY   STATUS             RESTARTS       AGE    IP            NODE       NOMINATED NODE   READINESS GATES
hello-node-cdcf64657-9chvx          1/1     Running            0              3d1h   172.17.0.9    minikube   <none>           <none>
my-dep-6d55d579d5-9xrx9             1/1     Running            2 (3d1h ago)   4d     172.17.0.2    minikube   <none>           <none>
nginx-deployment-5b4685b9bd-hhrrr   0/1     ImagePullBackOff   0              3d     172.17.0.11   minikube   <none>           <none>
nginx-deployment-ff6655784-4dk7k    1/1     Running            0              3d     172.17.0.10   minikube   <none>           <none>
nginx-deployment-ff6655784-thfjl    1/1     Running            0              3d     172.17.0.12   minikube   <none>           <none>
nginx-deployment-ff6655784-zg86c    1/1     Running            0              3d     172.17.0.13   minikube   <none>           <none>
pod1                                1/1     Running            2 (3d1h ago)   4d     172.17.0.4    minikube   <none>           <none>
pod2                                1/1     Running            2 (3d1h ago)   4d     172.17.0.5    minikube   <none>           <none>
```

`ubuntu@ubuntu-VM:~$ kubectl describe svc nginx`

```{r}
Error from server (NotFound): services "nginx" not found
```

`ubuntu@ubuntu-VM:~$ kubectl describe svc nginx -n test-2`

```{r}
Error from server (NotFound): namespaces "test-2" not found
```

`ubuntu@ubuntu-VM:~$ kubectl scale deploy nginx --replicas=3`

```{r}
Error from server (NotFound): deployments.apps "nginx" not found
```

`ubuntu@ubuntu-VM:~$ kubectl get deployments`

```{r}
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
hello-node         1/1     1            1           3d1h
my-dep             1/1     1            1           4d
nginx-deployment   3/3     1            3           3d
```

`ubuntu@ubuntu-VM:~$ kubectl scale deploy nginx-deployment --replicas=3`

```{r}
deployment.apps/nginx-deployment scaled
```

`ubuntu@ubuntu-VM:~$ kubectl create deploy nginx-deployment --image=nginx -n  training-2`

```{r}
deployment.apps/nginx-deployment created
```

`ubuntu@ubuntu-VM:~$ kubectl get deployment  -n  training-2`

```{r}
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
nginx-deployment   1/1     1            1           11s
nginxcip           1/1     1            1   
```

`ubuntu@ubuntu-VM:~$ kubectl expose deploy nginx-deployment --port=80 --type=NodePort  -n  training-2`

```{r}
service/nginx-deployment exposed
```

`ubuntu@ubuntu-VM:~$ kubectl get svc -n  training-2`

```{r}
NAME               TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
nginx-deployment   NodePort    10.106.153.204   <none>        80:32397/TCP   10s
nginxcip           ClusterIP   10.103.225.181   <none>        80/TCP         34m
```

`ubuntu@ubuntu-VM:~$ curl localhost:32397`

```{r}
curl: (7) Failed to connect to localhost port 32397 after 0 ms: Connection refused
```

`ubuntu@ubuntu-VM:~$ kubectl get nodes --output wide`

```{r}
NAME       STATUS   ROLES                  AGE    VERSION    INTERNAL-IP    EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION     CONTAINER-RUNTIME
minikube   Ready    control-plane,master   224d   v1.23.12   192.168.49.2   <none>        Ubuntu 20.04.5 LTS   6.2.0-34-generic   docker://20.10.23
```

`ubuntu@ubuntu-VM:~$ curl 192.168.49.2:32397`

```{r}
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>

```

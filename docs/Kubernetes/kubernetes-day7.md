# Kubernetes Day 7

`ubuntu@ubuntu-VM:~$ /opt/autonet.sh`

```{r}

----------------------------------
Script for Internet access
----------------------------------

Please enter your credentials:

Username (Name_Surname): rahul_vishwakarma1
Password:
For HJ,PT,NG and BR locations select 1
For BG,GOA,BLR,HYD locations select 2

Please enter the number: 1

1) For Hinjawdi Location press 1
2) For Pune Location press 2
3) For Nagpur Location press 3
4) For Blue Ridge Location press 4

Please enter Work location : 1
----------------------------------
Hinjawdi Location

.
--2023-11-07 10:17:33--  http://www.google.com/
Resolving www.google.com (www.google.com)... 172.217.166.36, 2404:6800:4009:80c::2004
Connecting to www.google.com (www.google.com)|172.217.166.36|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: unspecified [text/html]
Saving to: ‘index.html.58’

index.html.58           [ <=>                ]  20.33K  --.-KB/s    in 0.06s

2023-11-07 10:17:34 (313 KB/s) - ‘index.html.58’ saved [20813]

Connected to Internet.
```

`ubuntu@ubuntu-VM:~$ minikube start`

```{r}

* minikube v1.29.0 on Ubuntu 22.04
* Kubernetes 1.26.1 is now available. If you would like to upgrade, specify: --kubernetes-version=v1.26.1
* Using the docker driver based on existing profile
* Starting control plane node minikube in cluster minikube
* Pulling base image ...
* Updating the running docker "minikube" container ...
* minikube 1.31.2 is available! Download it: https://github.com/kubernetes/minikube/releases/tag/v1.31.2
* To disable this notice, run: 'minikube config set WantUpdateNotification false'

* Preparing Kubernetes v1.23.12 on Docker 20.10.23 ...
* Verifying Kubernetes components...
  - Using image gcr.io/k8s-minikube/storage-provisioner:v5
  - Using image docker.io/kubernetesui/dashboard:v2.7.0
  - Using image docker.io/kubernetesui/metrics-scraper:v1.0.8
* Some dashboard features require the metrics-server addon. To enable all features please run:

        minikube addons enable metrics-server


* Enabled addons: storage-provisioner, default-storageclass, dashboard

! /usr/bin/kubectl is version 1.26.3, which may have incompatibilities with Kubernetes 1.23.12.
  - Want kubectl v1.23.12? Try 'minikube kubectl -- get pods -A'
* Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
```

`ubuntu@ubuntu-VM:~$ kubectl get ns`

```{r}

NAME                   STATUS   AGE
default                Active   225d
kube-node-lease        Active   225d
kube-public            Active   225d
kube-system            Active   225d
kubernetes-dashboard   Active   4d
novgems                Active   6d
test                   Active   6d23h
training-2             Active   22h
```

`ubuntu@ubuntu-VM:~$ kubectl create ns test2`

```{r}
namespace/test2 created
```

`ubuntu@ubuntu-VM:~$ kubectl create deploy nginx-dep --image=nginx`

```{r}
deployment.apps/nginx-dep created
```

`ubuntu@ubuntu-VM:~$ kubectl get deployment -n test2`

```{r}
No resources found in test2 namespace.
```

`ubuntu@ubuntu-VM:~$ kubectl get deployment`

```{r}
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
hello-node         1/1     1            1           4d
my-dep             1/1     1            1           4d22h
nginx-dep          1/1     1            1           48s
nginx-deployment   3/3     1            3           3d23h
```

`ubuntu@ubuntu-VM:~$ kubectl create deploy nginx-dep --image=nginx -n test2`

```{r}
deployment.apps/nginx-dep created
```

`ubuntu@ubuntu-VM:~$ kubectl get deployment -n test2`

```{r}
NAME        READY   UP-TO-DATE   AVAILABLE   AGE
nginx-dep   1/1     1            1           17s
```

`ubuntu@ubuntu-VM:~$ kubectl delete ns test2`

```{r}
namespace "test2" deleted
```

`ubuntu@ubuntu-VM:~$ kubectl get deployment -n test2`

```{r}
No resources found in test2 namespace.
```

`ubuntu@ubuntu-VM:~$ kubectl create ns test2`

```{r}
namespace/test2 created
```

`ubuntu@ubuntu-VM:~$ kubectl get svc`

```{r}
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   225d
```

`ubuntu@ubuntu-VM:~$ kubectl get svc -n test2`

```{r}
No resources found in test2 namespace.
```

`ubuntu@ubuntu-VM:~$ kubectl create deploy nginx-dep --image=nginx -n test2`

```{r}
deployment.apps/nginx-dep created
```

`ubuntu@ubuntu-VM:~$ kubectl create expose nginx-dep --port=80 --type=NodePort -n test2`

```{r}
error: unknown flag: --port
See 'kubectl create --help' for usage.
```

`ubuntu@ubuntu-VM:~$ kubectl expose nginx-dep --port=80 --type=NodePort -n test2`

```{r}
error: the server doesn't have a resource type "nginx-dep"
```

`ubuntu@ubuntu-VM:~$ kubectl get deployment -n test2`

```{r}
NAME        READY   UP-TO-DATE   AVAILABLE   AGE
nginx-dep   1/1     1            1           87s
```

`ubuntu@ubuntu-VM:~$ kubectl expose deploy nginx-dep --port=80 --type=NodePort -n test2`

```{r}
service/nginx-dep exposed
```

`ubuntu@ubuntu-VM:~$ kubectl get svc -n test2`

```{r}
NAME        TYPE       CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
nginx-dep   NodePort   10.107.178.192   <none>        80:30776/TCP   47s
```

`ubuntu@ubuntu-VM:~$ kubectl get node -n test2`

```{r}
NAME       STATUS   ROLES                  AGE    VERSION
minikube   Ready    control-plane,master   225d   v1.23.12
```

`ubuntu@ubuntu-VM:~$ kubectl delete ns test2`

```{r}
namespace "test2" deleted
```

`ubuntu@ubuntu-VM:~$ kubectl get svc -n test2`

```{r}

No resources found in test2 namespace.
```

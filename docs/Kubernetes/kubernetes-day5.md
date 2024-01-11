`ubuntu@ubuntu-VM:~$ start minikube`
```{r}
Command 'start' not found, did you mean:
  command 'stars' from snap stars (2.7jrc3)
  command 'stat' from deb coreutils (8.32-4.1ubuntu1)
  command 'startx' from deb xinit (1.4.1-0ubuntu4)
  command 'tart' from deb tart (3.10-1build1)
  command 'rstart' from deb x11-session-utils (7.7+4build2)
  command 'kstart' from deb kde-cli-tools (4:5.24.4-0ubuntu1)
See 'snap info <snapname>' for additional versions.
```


`ubuntu@ubuntu-VM:~$ minikube start`
```{r}
* minikube v1.29.0 on Ubuntu 22.04
* Kubernetes 1.26.1 is now available. If you would like to upgrade, ubernetes-version=v1.26.1
* minikube 1.31.2 is available! Download it: https://github.com/kubeube/releases/tag/v1.31.2
* To disable this notice, run: 'minikube config set WantUpdateNotifi'

* Using the docker driver based on existing profile
* Starting control plane node minikube in cluster minikube
* Pulling base image ...
* Updating the running docker "minikube" container ...
* Preparing Kubernetes v1.23.12 on Docker 20.10.23 ...
* Verifying Kubernetes components...
  - Using image gcr.io/k8s-minikube/storage-provisioner:v5
* Enabled addons: storage-provisioner, default-storageclass

! /usr/bin/kubectl is version 1.26.3, which may have incompatibilitirnetes 1.23.12.
  - Want kubectl v1.23.12? Try 'minikube kubectl -- get pods -A'
* Done! kubectl is now configured to use "minikube" cluster and "deface by default
```


`ubuntu@ubuntu-VM:~$ minikube dashboard`
```{r}
* Enabling dashboard ...
  - Using image docker.io/kubernetesui/dashboard:v2.7.0
  - Using image docker.io/kubernetesui/metrics-scraper:v1.0.8
* Some dashboard features require the metrics-server addon. To enable all features please run:

        minikube addons enable metrics-server


* Verifying dashboard health ...
* Launching proxy ...
* Verifying proxy health ...
* Opening http://127.0.0.1:39617/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/ in your default browser...
/usr/bin/xdg-open: 882: www-browser: not found
/usr/bin/xdg-open: 882: links2: not found
/usr/bin/xdg-open: 882: elinks: not found
/usr/bin/xdg-open: 882: links: not found
/usr/bin/xdg-open: 882: lynx: not found
/usr/bin/xdg-open: 882: w3m: not found
xdg-open: no method available for opening 'http://127.0.0.1:39617/api/v1/namespaces/kubernetes-dashboard/services/http:kubernetes-dashboard:/proxy/'

X Exiting due to HOST_BROWSER: failed to open browser: exit status 3

```


`ubuntu@ubuntu-VM:~$ kubectl create deployment`
```{r}
 hello-node --image=registry.k8s.io/e2e-test-images/agnhost:2.39 -- /agnhost netexec --http-port=8080
deployment.apps/hello-node created
```

`ubuntu@ubuntu-VM:~$ kubectl get deployments`
```{r}

NAME         READY   UP-TO-DATE   AVAILABLE   AGE
hello-node   1/1     1            1           13s
my-dep       1/1     1            1           22h
```

`ubuntu@ubuntu-VM:~$ kubectl get pods`
```{r}
NAME                         READY   STATUS    RESTARTS      AGE
hello-node-cdcf64657-9chvx   1/1     Running   0             20s
my-dep-6d55d579d5-9xrx9      1/1     Running   2 (19m ago)   22h
pod1                         1/1     Running   2 (19m ago)   23h
pod2                         1/1     Running   2 (19m ago)   23h
```


`ubuntu@ubuntu-VM:~$ kubectl get events`
```{r}
LAST SEEN   TYPE      REASON              OBJECT                            MESSAGE
36s         Normal    Scheduled           pod/hello-node-cdcf64657-9chvx    Successfully assigned default/hello-node-cdcf64657-9chvx to minikube
35s         Normal    Pulling             pod/hello-node-cdcf64657-9chvx    Pulling image "registry.k8s.io/e2e-test-images/agnhost:2.39"
29s         Normal    Pulled              pod/hello-node-cdcf64657-9chvx    Successfully pulled image "registry.k8s.io/e2e-test-images/agnhost:2.39" in 6.527180476s
28s         Normal    Created             pod/hello-node-cdcf64657-9chvx    Created container agnhost
28s         Normal    Started             pod/hello-node-cdcf64657-9chvx    Started container agnhost
36s         Normal    SuccessfulCreate    replicaset/hello-node-cdcf64657   Created pod: hello-node-cdcf64657-9chvx
36s         Normal    ScalingReplicaSet   deployment/hello-node             Scaled up replica set hello-node-cdcf64657 to 1
19m         Normal    Starting            node/minikube             
18m         Normal    RegisteredNode      node/minikube                     Node minikube event: Registered Node minikube in Controller
19m         Normal    Pulling             pod/my-dep-6d55d579d5-9xrx9       Pulling image "nginx"
19m         Normal    Created             pod/my-dep-6d55d579d5-9xrx9       Created container nginx
19m         Normal    Started             pod/my-dep-6d55d579d5-9xrx9       Started container nginx
19m         Normal    SandboxChanged      pod/my-dep-6d55d579d5-9xrx9       Pod sandbox changed, it will be killed and re-created.
19m         Normal    Pulled              pod/my-dep-6d55d579d5-9xrx9       Successfully pulled image "nginx" in 2.74658657s
19m         Warning   FailedSync          pod/my-dep-6d55d579d5-9xrx9       error determining status: rpc error: code = Unknown desc = Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?
19m         Normal    Pulled              pod/my-dep-6d55d579d5-9xrx9       Successfully pulled image "nginx" in 2.774821453s
19m         Normal    Pulled              pod/pod1                          Container image "gcr.io/google-samples/hello-app:2.0" already present on machine
19m         Normal    Created             pod/pod1                          Created container hello1
19m         Normal    Started             pod/pod1                          Started container hello1
19m         Normal    SandboxChanged      pod/pod1                          Pod sandbox changed, it will be killed and re-created.
19m         Normal    Pulled              pod/pod2                          Container image "gcr.io/google-samples/hello-app:1.0" already present on machine
19m         Normal    Created             pod/pod2                          Created container hello2
19m         Normal    Started             pod/pod2                          Started container hello2
19m         Normal    SandboxChanged      pod/pod2                          Pod sandbox changed, it will be killed and re-created.
19m         Warning   FailedSync          pod/pod2                          error determining status: rpc error: code = Unknown desc = Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?
```


`ubuntu@ubuntu-VM:~$ kubectl config view`
```{r}
apiVersion: v1
clusters:
- cluster:
    certificate-authority: /home/ubuntu/.minikube/ca.crt
    extensions:
    - extension:
        last-update: Fri, 03 Nov 2023 09:51:02 IST
        provider: minikube.sigs.k8s.io
        version: v1.29.0
      name: cluster_info
    server: https://192.168.49.2:8443
  name: minikube
contexts:
- context:
    cluster: minikube
    extensions:
    - extension:
        last-update: Fri, 03 Nov 2023 09:51:02 IST
        provider: minikube.sigs.k8s.io
        version: v1.29.0
      name: context_info
    namespace: default
    user: minikube
  name: minikube
current-context: minikube
kind: Config
preferences: {}
users:
- name: minikube
  user:
    client-certificate: /home/ubuntu/.minikube/profiles/minikube/client.crt
    client-key: /home/ubuntu/.minikube/profiles/minikube/client.key
```


`ubuntu@ubuntu-VM:~$
kubectl logs hello-node-cdcf64657-9chvx`
```{r}
I1103 04:39:41.218384       1 log.go:195] Started HTTP server on port 8080
I1103 04:39:41.218975       1 log.go:195] Started UDP server on port  8081
```


`ubuntu@ubuntu-VM:~$ kubectl proxy`
```{r}
Starting to serve on 127.0.0.1:8001

<--------new session---------->

```


`ubuntu@ubuntu-VM:~$ curl http://localhost:8001/version`
```{r}

{
  "major": "1",
  "minor": "23",
  "gitVersion": "v1.23.12",
  "gitCommit": "c6939792865ef0f70f92006081690d77411c8ed5",
  "gitTreeState": "clean",
  "buildDate": "2022-09-21T12:13:07Z",
  "goVersion": "go1.17.13",
  "compiler": "gc",
  "platform": "linux/amd64"
```

`ubuntu@ubuntu-VM:~$ kubectl apply -f https://k8s.io/examples/controllers/nginx-deployment.yaml`

```{r}
deployment.apps/nginx-deployment created
```


`ubuntu@ubuntu-VM:~$ kubectl get deployments`
```{r}
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
hello-node         1/1     1            1           54m
my-dep             1/1     1            1           23h
nginx-deployment   3/3     3            3           16s
```


`ubuntu@ubuntu-VM:~$ kubectl rollout status deployment/nginx-deployment`
```{r}
deployment "nginx-deployment" successfully rolled out
```


`ubuntu@ubuntu-VM:~$ kubectl get rs`
```{r}

NAME                         DESIRED   CURRENT   READY   AGE
frontend                     2         2         2       23h
hello-node-cdcf64657         1         1         1       55m
my-dep-6d55d579d5            1         1         1       23h
nginx-deployment-9456bbbf9   3         3         3       86s
```

`ubuntu@ubuntu-VM:~$ kubectl get pods --show-labels`
```{r}
NAME                               READY   STATUS    RESTARTS      A                                                                                                    GE    LABELS
hello-node-cdcf64657-9chvx         1/1     Running   0             5                                                                                                    6m    app=hello-node,pod-template-hash=cdcf64657
my-dep-6d55d579d5-9xrx9            1/1     Running   2 (75m ago)   2                                                                                                    3h    app=my-dep,pod-template-hash=6d55d579d5
nginx-deployment-9456bbbf9-7hkg5   1/1     Running   0             1                                                                                                    13s   app=nginx,pod-template-hash=9456bbbf9
nginx-deployment-9456bbbf9-fgmhc   1/1     Running   0             1                                                                                                    13s   app=nginx,pod-template-hash=9456bbbf9
nginx-deployment-9456bbbf9-ndxrr   1/1     Running   0             1                                                                                                    13s   app=nginx,pod-template-hash=9456bbbf9
pod1                               1/1     Running   2 (75m ago)   2                                                                                                    4h    tier=frontend
pod2                               1/1     Running   2 (75m ago)   2                                                                                                    4h    tier=frontend
```


`ubuntu@ubuntu-VM:~$ kubectl set image deployment.v1.apps/nginx-deployment nginx=nginx:1.16.1`
```{r}
deployment.apps/nginx-deployment image updated
```


`ubuntu@ubuntu-VM:~$ kubectl edit deployment/nginx-deployment`
```{r}
Edit cancelled, no changes made.
```


`ubuntu@ubuntu-VM:~$ kubectl rollout status deployment/nginx-deployment`
```{r}
deployment "nginx-deployment" successfully rolled out
```


`ubuntu@ubuntu-VM:~$ kubectl get rs`
```{r}

NAME                         DESIRED   CURRENT   READY   AGE
frontend                     2         2         2       23h
hello-node-cdcf64657         1         1         1       58m
my-dep-6d55d579d5            1         1         1       23h
nginx-deployment-9456bbbf9   0         0         0       4m15s
nginx-deployment-ff6655784   3         3         3       107s
```

`ubuntu@ubuntu-VM:~$ kubectl get pods`
```{r}
NAME                               READY   STATUS    RESTARTS      AGE
hello-node-cdcf64657-9chvx         1/1     Running   0             59m
my-dep-6d55d579d5-9xrx9            1/1     Running   2 (77m ago)   23h
nginx-deployment-ff6655784-4dk7k   1/1     Running   0             109s
nginx-deployment-ff6655784-thfjl   1/1     Running   0             108s
nginx-deployment-ff6655784-zg86c   1/1     Running   0             2m
pod1                               1/1     Running   2 (77m ago)   24h
pod2                               1/1     Running   2 (77m ago)   24h
```


`ubuntu@ubuntu-VM:~$ kubectl describe deployments`
```{r}

```


`ubuntu@ubuntu-VM:~$ kubectl set image deployment/nginx-deployment nginx=nginx:1.161`
```{r}
Name:                   hello-node
Namespace:              default
CreationTimestamp:      Fri, 03 Nov 2023 10:09:33 +0530
Labels:                 app=hello-node
Annotations:            deployment.kubernetes.io/revision: 1
Selector:               app=hello-node
Replicas:               1 desired | 1 updated | 1 total | 1 available | 0 un                                                                                            available
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=hello-node
  Containers:
   agnhost:
    Image:      registry.k8s.io/e2e-test-images/agnhost:2.39
    Port:       <none>
    Host Port:  <none>
    Command:
      /agnhost
      netexec
      --http-port=8080
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      True    MinimumReplicasAvailable
  Progressing    True    NewReplicaSetAvailable
OldReplicaSets:  <none>
NewReplicaSet:   hello-node-cdcf64657 (1/1 replicas created)
Events:
  Type    Reason             Age   From                   Message
  ----    ------             ----  ----                   -------
  Normal  ScalingReplicaSet  60m   deployment-controller  Scaled up replica                                                                                             set hello-node-cdcf64657 to 1


Name:                   my-dep
Namespace:              default
CreationTimestamp:      Thu, 02 Nov 2023 11:48:25 +0530
Labels:                 app=my-dep
Annotations:            deployment.kubernetes.io/revision: 1
Selector:               app=my-dep
Replicas:               1 desired | 1 updated | 1 total | 1 available | 0 un                                                                                            available
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=my-dep
  Containers:
   nginx:
    Image:        nginx
    Port:         8080/TCP
    Host Port:    0/TCP
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      True    MinimumReplicasAvailable
  Progressing    True    NewReplicaSetAvailable
OldReplicaSets:  <none>
NewReplicaSet:   my-dep-6d55d579d5 (1/1 replicas created)
Events:          <none>


Name:                   nginx-deployment
Namespace:              default
CreationTimestamp:      Fri, 03 Nov 2023 11:04:06 +0530
Labels:                 app=nginx
Annotations:            deployment.kubernetes.io/revision: 2
Selector:               app=nginx
Replicas:               3 desired | 3 updated | 3 total | 3 available | 0 un                                                                                            available
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  25% max unavailable, 25% max surge
Pod Template:
  Labels:  app=nginx
  Containers:
   nginx:
    Image:        nginx:1.16.1
    Port:         80/TCP
    Host Port:    0/TCP
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      True    MinimumReplicasAvailable
  Progressing    True    NewReplicaSetAvailable
OldReplicaSets:  <none>
NewReplicaSet:   nginx-deployment-ff6655784 (3/3 replicas created)
Events:
  Type    Reason             Age    From                   Message
  ----    ------             ----   ----                   -------
  Normal  ScalingReplicaSet  5m41s  deployment-controller  Scaled up replica                                                                                             set nginx-deployment-9456bbbf9 to 3
  Normal  ScalingReplicaSet  3m13s  deployment-controller  Scaled up replica                                                                                             set nginx-deployment-ff6655784 to 1
  Normal  ScalingReplicaSet  3m2s   deployment-controller  Scaled down repli                                                                                            ca set nginx-deployment-9456bbbf9 to 2
  Normal  ScalingReplicaSet  3m2s   deployment-controller  Scaled up replica                                                                                             set nginx-deployment-ff6655784 to 2
  Normal  ScalingReplicaSet  3m1s   deployment-controller  Scaled down repli                                                                                            ca set nginx-deployment-9456bbbf9 to 1
  Normal  ScalingReplicaSet  3m1s   deployment-controller  Scaled up replica                                                                                             set nginx-deployment-ff6655784 to 3
  Normal  ScalingReplicaSet  3m     deployment-controller  Scaled down repli                                                                                            ca set nginx-deployment-9456bbbf9 to 0
  deployment.apps/nginx-deployment image updated
```


`ubuntu@ubuntu-VM:~$ kubectl rollout status deployment/nginx-deployment`
```{r}
Waiting for deployment "nginx-deployment" rollout to finish: 1 out of 3 new                                                                                             replicas have been updated...
```

`ubuntu@ubuntu-VM:~$ kubectl rollout status deployment/nginx-deployment`
```{r}
Waiting for deployment "nginx-deployment" rollout to finish: 1 out of 3 new                                                                                             replicas have been updated...
^C
```


`ubuntu@ubuntu-VM:~$ kubectl rollout status deployment/nginx-deployment`
```{r}

Waiting for deployment "nginx-deployment" rollout to finish: 1 out of 3 new                                                                                             replicas have been updated...
```

`ubuntu@ubuntu-VM:~$ $ kubectget rs`
```{r}

NAME                          DESIRED   CURRENT   READY   AGE
frontend                      2         2         2       24h
hello-node-cdcf64657          1         1         1       66m
my-dep-6d55d579d5             1         1         1       23h
nginx-deployment-5b4685b9bd   1         1         0       5m30s
nginx-deployment-9456bbbf9    0         0         0       12m
nginx-deployment-ff6655784    3         3         3       9m34s

```

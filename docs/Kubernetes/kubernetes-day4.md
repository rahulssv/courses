# Kubernetes Day 4
`ubuntu@ubuntu-VM:~$ minikube start`
```{r}
* minikube v1.29.0 on Ubuntu 22.04
* Kubernetes 1.26.1 is now available. If you would like to upgrad   e, specify: --kubernetes-version=v1.26.1
* Using the docker driver based on existing profile
* Starting control plane node minikube in cluster minikube
* Pulling base image ...
* Updating the running docker "minikube" container ...
! This container is having trouble accessing https://k8s.gcr.io
* To pull new external images, you may need to configure a proxy:    https://minikube.sigs.k8s.io/docs/reference/networking/proxy/
* Preparing Kubernetes v1.23.12 on Docker 20.10.23 ...
* Verifying Kubernetes components...
  - Using image gcr.io/k8s-minikube/storage-provisioner:v5
* Enabled addons: default-storageclass, storage-provisioner

! /usr/bin/kubectl is version 1.26.3, which may have incompatibilities with Kubernetes 1.23.12.
  - Want kubectl v1.23.12? Try 'minikube kubectl -- get pods -A'
* Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
```
`ubuntu@ubuntu-VM:~$ kube ctl get pods`
```{r}
Command 'kube' not found, did you mean:
  command 'kubu' from snap kubu (1.1.4)
  command 'jube' from deb jube (2.4.2-1)
  command 'qube' from deb avogadro-utils (1.95.1-8)
See 'snap info <snapname>' for additional versions.
```
`ubuntu@ubuntu-VM:~$ kubectl get pods`
```{r}
NAME            READY   STATUS    RESTARTS         AGE
twocontainers   2/2     Running   10 (2m19s ago)   22h
```
`ubuntu@ubuntu-VM:~$ kubectl delete pod ```{r}
twocontainers`
pod "twocontainers" deleted

```
`ubuntu@ubuntu-VM:~$ kubectl get pods`
```{r}
No resources found in default namespace.
```
`ubuntu@ubuntu-VM:~$ kubectl apply -f https://kubernetes.io/examples/ontend.yaml`
```{r}
replicaset.apps/frontend created
```

`ubuntu@ubuntu-VM:~$ kubectl get rs`
```{r}
NAME       DESIRED   CURRENT   READY   AGE
frontend   3         3         0       17s
```
`ubuntu@ubuntu-VM:~$ kubectl describe rs/frontend`
```{r}
Name:         frontend
Namespace:    default
Selector:     tier=frontend
Labels:       app=guestbook
              tier=frontend
Annotations:  <none>
Replicas:     3 current / 3 desired
Pods Status:  3 Running / 0 Waiting / 0 Succeeded / 0 Failed
Pod Template:
  Labels:  tier=frontend
  Containers:
   php-redis:
    Image:        gcr.io/google_samples/gb-frontend:v3
    Port:         <none>
    Host Port:    <none>
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Events:
  Type    Reason            Age   From                   Message
  ----    ------            ----  ----                   -------
  Normal  SuccessfulCreate  52s   replicaset-controller  Created poddt
  Normal  SuccessfulCreate  52s   replicaset-controller  Created pod52
  Normal  SuccessfulCreate  52s   replicaset-controller  Created podfm
```
`ubuntu@ubuntu-VM:~$ kubectl get pods`
```{r}
NAME             READY   STATUS    RESTARTS   AGE
frontend-bh4fm   1/1     Running   0          98s
frontend-lmk52   1/1     Running   0          98s
frontend-q6xdt   1/1     Running   0          98s

````ubuntu@ubuntu-VM:~$ kubectl get pods frontend-b2zdv -o yaml`
```{r}
Error from server (NotFound): pods "frontend-b2zdv" not found

```
`ubuntu@ubuntu-VM:~$ kubectl get pods frontend-bh4fm -o yaml`
```{r}
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: "2023-11-02T04:37:41Z"
  generateName: frontend-
  labels:
    tier: frontend
  name: frontend-bh4fm
  namespace: default
  ownerReferences:
  - apiVersion: apps/v1
    blockOwnerDeletion: true
    controller: true
    kind: ReplicaSet
    name: frontend
    uid: e961c8fd-3ea7-4572-9270-cda6b24309d9
  resourceVersion: "187365"
  uid: 6ff854b5-f861-433c-aba7-857091da35ad
spec:
  containers:
  - image: gcr.io/google_samples/gb-frontend:v3
    imagePullPolicy: IfNotPresent
    name: php-redis
    resources: {}
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: kube-api-access-r928w
      readOnly: true
  dnsPolicy: ClusterFirst
  enableServiceLinks: true
  nodeName: minikube
  preemptionPolicy: PreemptLowerPriority
  priority: 0
  restartPolicy: Always
  schedulerName: default-scheduler
  securityContext: {}
  serviceAccount: default
  serviceAccountName: default
  terminationGracePeriodSeconds: 30
  tolerations:
  - effect: NoExecute
    key: node.kubernetes.io/not-ready
    operator: Exists
    tolerationSeconds: 300
  - effect: NoExecute
    key: node.kubernetes.io/unreachable
    operator: Exists
    tolerationSeconds: 300
  volumes:
  - name: kube-api-access-r928w
    projected:
      defaultMode: 420
      sources:
      - serviceAccountToken:
          expirationSeconds: 3607
          path: token
      - configMap:
          items:
          - key: ca.crt
            path: ca.crt
          name: kube-root-ca.crt
      - downwardAPI:
          items:
          - fieldRef:
              apiVersion: v1
              fieldPath: metadata.namespace
            path: namespace
status:
  conditions:
  - lastProbeTime: null
    lastTransitionTime: "2023-11-02T04:37:41Z"
    status: "True"
    type: Initialized
  - lastProbeTime: null
    lastTransitionTime: "2023-11-02T04:38:05Z"
    status: "True"
    type: Ready
  - lastProbeTime: null
    lastTransitionTime: "2023-11-02T04:38:05Z"
    status: "True"
    type: ContainersReady
  - lastProbeTime: null
    lastTransitionTime: "2023-11-02T04:37:41Z"
    status: "True"
    type: PodScheduled
  containerStatuses:
  - containerID: docker://bd9b381d8404c84095ae265baa913d4cd0fa00505d3ce9e7ff
    image: gcr.io/google_samples/gb-frontend:v3
    imageID: docker-pullable://gcr.io/google_samples/gb-frontend@shaf6a18586d6751e8963cf684c27b9873ca926df22cdf88ed4452615
    lastState: {}
    name: php-redis
    ready: true
    restartCount: 0
    started: true
    state:
      running:
        startedAt: "2023-11-02T04:38:04Z"
  hostIP: 192.168.49.2
  phase: Running
  podIP: 172.17.0.2
  podIPs:
  - ip: 172.17.0.2
  qosClass: BestEffort
  startTime: "2023-11-02T04:37:41Z"

```
`ubuntu@ubuntu-VM:~$ kubectl apply -f https://kubernetes.io/examples/ml`
```{r}
pod/pod1 created
pod/pod2 created
```

`ubuntu@ubuntu-VM:~$ kubectl get pods`
```{r}
NAME             READY   STATUS    RESTARTS   AGE
frontend-bh4fm   1/1     Running   0          54m
frontend-lmk52   1/1     Running   0          54m
frontend-q6xdt   1/1     Running   0          54m

```
`ubuntu@ubuntu-VM:~$ kubectl get pods`
```{r}
NAME             READY   STATUS    RESTARTS   AGE
frontend-bh4fm   1/1     Running   0          55m
frontend-lmk52   1/1     Running   0          55m
frontend-q6xdt   1/1     Running   0          55m

```
`ubuntu@ubuntu-VM:~$ kubectl apply -f https://kubernetes.io/examples/ml`
```{r}
pod/pod1 created
pod/pod2 created
```
`ubuntu@ubuntu-VM:~$ kubectl apply -f https://kubernetes.io/examples/ontend.yaml`
```{r}
replicaset.apps/frontend unchanged
```
`ubuntu@ubuntu-VM:~$ kubectl get pods`
```{r}
NAME             READY   STATUS    RESTARTS   AGE
frontend-bh4fm   1/1     Running   0          55m
frontend-lmk52   1/1     Running   0          55m
frontend-q6xdt   1/1     Running   0          55m
```
`ubuntu@ubuntu-VM:~$ kubectl delete rs frontend`
```{r}
replicaset.apps "frontend" deleted
```
`ubuntu@ubuntu-VM:~$ kubectl get pods`
```{r}
No resources found in default namespace.
```
`ubuntu@ubuntu-VM:~$ kubectl apply -f https://kubernetes.io/examples/ml`
```{r}
pod/pod1 created
pod/pod2 created
```
`ubuntu@ubuntu-VM:~$ kubectl get pods`
```{r}
NAME   READY   STATUS    RESTARTS   AGE
pod1   1/1     Running   0          4s
pod2   1/1     Running   0          4s
```
`ubuntu@ubuntu-VM:~$ touch frontendrs.yml`
`ubuntu@ubuntu-VM:~$ nano frontendrs.yml`
`ubuntu@ubuntu-VM:~$ kubectl create -f frontendrs.yml`
```{r}
replicaset.apps/frontend created
```
`ubuntu@ubuntu-VM:~$ kubectl get pods`
```{r}
NAME   READY   STATUS    RESTARTS   AGE
pod1   1/1     Running   0          4m10s
pod2   1/1     Running   0          4m10s
```
`ubuntu@ubuntu-VM:~$ kubectl get rs`
```{r}
NAME       DESIRED   CURRENT   READY   AGE
frontend   2         2         2       15s
```
`ubuntu@ubuntu-VM:~$ kubectl describe rs/frontend`
```{r}
Name:         frontend
Namespace:    default
Selector:     tier=frontend
Labels:       app=guestbook
              tier=frontend
Annotations:  <none>
Replicas:     2 current / 2 desired
Pods Status:  2 Running / 0 Waiting / 0 Succeeded / 0 Failed
Pod Template:
  Labels:  tier=frontend
  Containers:
   php-redis:
    Image:        gcr.io/google_samples/gb-frontend:v3
    Port:         <none>
    Host Port:    <none>
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Events:           <none>

```
`ubuntu@ubuntu-VM:~$ kubectl create deployment --help`
```{r}
Create a deployment with the specified name.

Aliases:
deployment, deploy

Examples:
  # Create a deployment named my-dep that runs the busybox image
  kubectl create deployment my-dep --image=busybox

  # Create a deployment with a command
  kubectl create deployment my-dep --image=busybox -- date

  # Create a deployment named my-dep that runs the nginx image with 3 replicas
  kubectl create deployment my-dep --image=nginx --replicas=3

  # Create a deployment named my-dep that runs the busybox image and expose port 5701
  kubectl create deployment my-dep --image=busybox --port=5701

Options:
    --allow-missing-template-keys=true:
        If true, ignore any errors in templates when a field or map key is missing in the template. Only applies to golang and jsonpath output formats.

    --dry-run='none':
        Must be "none", "server", or "client". If client strategy, only print the object that would be sent, without sending it. If server strategy, submit server-side request without persisting the resource.

    --field-manager='kubectl-create':
        Name of the manager used to track field ownership.

    --image=[]:
        Image names to run.

    -o, --output='':
        Output format. One of: (json, yaml, name, go-template, go-template-file, template, templatefile, jsonpath, jsonpath-as-json, jsonpath-file).

    --port=-1:
        The port that this container exposes.

    -r, --replicas=1:
        Number of replicas to create. Default is 1.

    --save-config=false:
        If true, the configuration of current object will be saved in its annotation. Otherwise, the annotation will be unchanged. This flag is useful when you want to perform kubectl apply on this object in the future.

    --show-managed-fields=false:
        If true, keep the managedFields when printing objects in JSON or YAML format.

    --template='':
        Template string or path to template file to use when -o=go-template, -o=go-template-file. The template format is golang templates [http://golang.org/pkg/text/template/#pkg-overview].

    --validate='strict':
        Must be one of: strict (or true), warn, ignore (or false). "true" or "strict" will use a schema to validate the input and fail the request if invalid. It will perform server side validation if ServerSideFieldValidation is enabled on the api-server, but will fall back to less reliable client-side validation if not.             "warn" will warn about unknown or duplicate fields without blocking the request if server-side field validation is enabled on the API server, and behave as "ignore" otherwise.             "false" or "ignore" will not perform any schema validation, silently dropping any unknown or duplicate fields.

Usage:
  kubectl create deployment NAME --image=image -- [COMMAND] [args...] [options]

Use "kubectl options" for a list of global command-line options (applies to all commands).
```
`ubuntu@ubuntu-VM:~$ kubectl create deployment my-dep --image=nginx --port=8080`
```{r}
deployment.apps/my-dep created
```
`ubuntu@ubuntu-VM:~$ kubectl get deployment`
```{r}
NAME     READY   UP-TO-DATE   AVAILABLE   AGE
my-dep   1/1     1            1           40s
```
`ubuntu@ubuntu-VM:~$ curl localhost:8080`
```{r}
<html><head><meta http-equiv='refresh' content='1;url=/login?from=%2F'/><script>window.location.replace('/login?from=%2F');</script></head><body style='background-color:white; color:white;'>


Authentication required
<!--
-->

</body></html>                                                    
```
`ubuntu@ubuntu-VM:~$ kubectl get deployment`
```{r}
NAME     READY   UP-TO-DATE   AVAILABLE   AGE
my-dep   1/1     1            1           7m48s
```
`ubuntu@ubuntu-VM:~$ kubectl get pods`
```{r}
NAME                      READY   STATUS    RESTARTS   AGE
my-dep-6d55d579d5-9xrx9   1/1     Running   0          7m57s
pod1                      1/1     Running   0          51m
pod2                      1/1     Running   0          51m
```
`ubuntu@ubuntu-VM:~$ kubectl describe my-dep-6d55d579d5-9xrx9`
```{r}
error: the server doesn't have a resource type "my-dep-6d55d579d5-9xrx9"
```
`ubuntu@ubuntu-VM:~$ kubectl describe pod my-dep-6d55d579d5-9xrx9`
```{r}
Name:             my-dep-6d55d579d5-9xrx9
Namespace:        default
Priority:         0
Service Account:  default
Node:             minikube/192.168.49.2
Start Time:       Thu, 02 Nov 2023 11:48:25 +0530
Labels:           app=my-dep
                  pod-template-hash=6d55d579d5
Annotations:      <none>
Status:           Running
IP:               172.17.0.6
IPs:
  IP:           172.17.0.6
Controlled By:  ReplicaSet/my-dep-6d55d579d5
Containers:
  nginx:
    Container ID:   docker://f7d3a488297b7188275207dc5400ea08764d462d7c32c24104b50aa7aca155bf
    Image:          nginx
    Image ID:       docker-pullable://nginx@sha256:86e53c4c16a6a276b204b0fd3a8143d86547c967dc8258b3d47c3a21bb68d3c6
    Port:           8080/TCP
    Host Port:      0/TCP
    State:          Running
      Started:      Thu, 02 Nov 2023 11:48:40 +0530
    Ready:          True
    Restart Count:  0
    Environment:    <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-52dkp (ro)
Conditions:
  Type              Status
  Initialized       True
  Ready             True
  ContainersReady   True
  PodScheduled      True
Volumes:
  kube-api-access-52dkp:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
  Type    Reason     Age    From               Message
  ----    ------     ----   ----               -------
  Normal  Scheduled  8m35s  default-scheduler  Successfully assigned default/my-dep-6d55d579d5-9xrx9 to minikube
  Normal  Pulling    8m35s  kubelet            Pulling image "nginx"
  Normal  Pulled     8m22s  kubelet            Successfully pulled image "nginx" in 13.176684961s
  Normal  Created    8m21s  kubelet            Created container nginx
  Normal  Started    8m21s  kubelet            Started container nginx
```
`ubuntu@ubuntu-VM:~$ kubectl exec -it my-dep-6d55d579d5-9xrx9 -c nginx bash`
```{r}
kubectl exec [POD] [COMMAND] is DEPRECATED and will be removed in a future version. Use kubectl exec [POD] -- [COMMAND] instead.
root@my-dep-6d55d579d5-9xrx9:/# curl localhost
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
root@my-dep-6d55d579d5-9xrx9:/# exit
exit
```

`ubuntu@ubuntu-VM:~$ kubectl get cluster-info`
```{r}
error: the server doesn't have a resource type "cluster-info"
```
`ubuntu@ubuntu-VM:~$ kubectl cluster-info`
```{r}
Kubernetes control plane is running at https://192.168.49.2:8443
CoreDNS is running at https://192.168.49.2:8443/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.
```
`ubuntu@ubuntu-VM:~$ kubectl get nodes`
```{r}
NAME       STATUS   ROLES                  AGE    VERSION
minikube   Ready    control-plane,master   220d   v1.23.12
```
`ubuntu@ubuntu-VM:~$ kubectl get pods`
```{r}
NAME                      READY   STATUS    RESTARTS   AGE
my-dep-6d55d579d5-9xrx9   1/1     Running   0          36m
pod1                      1/1     Running   0          79m
pod2                      1/1     Running   0          79m
```
`ubuntu@ubuntu-VM:~$ kubectl get deployments`
```{r}
NAME     READY   UP-TO-DATE   AVAILABLE   AGE
my-dep   1/1     1            1           36m
```
`ubuntu@ubuntu-VM:~$ kubectl get svc`
```{r}
NAME         TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
kubernetes   ClusterIP   10.96.0.1    <none>        443/TCP   220d
```



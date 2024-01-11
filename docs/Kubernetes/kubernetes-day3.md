# Kubernetes Day 3

`ubuntu@ubuntu-VM:~$ minikube start`

```{r}
* minikube v1.29.0 on Ubuntu 22.04
* Kubernetes 1.26.1 is now available. If you would like to upgrade, specify: --kubernetes-version=v1.26.1
* Using the docker driver based on existing profile
* Starting control plane node minikube in cluster minikube
* Pulling base image ...
* Updating the running docker "minikube" container ...
* Preparing Kubernetes v1.23.12 on Docker 20.10.23 ...
* Verifying Kubernetes components...
  * Using image gcr.io/k8s-minikube/storage-provisioner:v5
* Enabled addons: storage-provisioner, default-storageclass

! /usr/bin/kubectl is version 1.26.3, which may have incompatibilities with Kubernetes 1.23.12.

* Want kubectl v1.23.12? Try 'minikube kubectl -- get pods -A'

* Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default

```

`ubuntu@ubuntu-VM:~$ vim`

```{r}
Command 'vim' not found, but can be installed with:
sudo apt install vim         # version 2:8.2.3995-1ubuntu2.13, or
sudo apt install vim-tiny    # version 2:8.2.3995-1ubuntu2.13
sudo apt install neovim      # version 0.6.1-3
sudo apt install vim-athena  # version 2:8.2.3995-1ubuntu2.13
sudo apt install vim-gtk3    # version 2:8.2.3995-1ubuntu2.13
sudo apt install vim-nox     # version 2:8.2.3995-1ubuntu2.13
```

`ubuntu@ubuntu-VM:~$ apt-get install vim`

```{r}
E: Could not open lock file /var/lib/dpkg/lock-frontend - open (13: Permission denied)
E: Unable to acquire the dpkg frontend lock (/var/lib/dpkg/lock-frontend), are you root?
```

`ubuntu@ubuntu-VM:~$ sudo apt-get install vim`

```{r}
[sudo] password for ubuntu:
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following packages were automatically installed and are no longer required:
  libflashrom1 libftdi1-2
Use 'sudo apt autoremove' to remove them.
The following additional packages will be installed:
  vim-runtime
Suggested packages:
  ctags vim-doc vim-scripts
The following NEW packages will be installed:
  vim vim-runtime
0 upgraded, 2 newly installed, 0 to remove and 30 not upgraded.
Need to get 8,568 kB of archives.
After this operation, 37.6 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 <http://in.archive.ubuntu.com/ubuntu> jammy-updates/main amd64 vim-runtime a                                                                                        ll 2:8.2.3995-1ubuntu2.13 [6,834 kB]
Get:2 <http://in.archive.ubuntu.com/ubuntu> jammy-updates/main amd64 vim amd64 2:8                                                                                        .2.3995-1ubuntu2.13 [1,734 kB]
Fetched 8,568 kB in 8s (1,050 kB/s)
Selecting previously unselected package vim-runtime.
(Reading database ... 208278 files and directories currently installed.)
Preparing to unpack .../vim-runtime_2%3a8.2.3995-1ubuntu2.13_all.deb ...
Adding 'diversion of /usr/share/vim/vim82/doc/help.txt to /usr/share/vim/vim82/d                                                                                        oc/help.txt.vim-tiny by vim-runtime'
Adding 'diversion of /usr/share/vim/vim82/doc/tags to /usr/share/vim/vim82/doc/t                                                                                        ags.vim-tiny by vim-runtime'
Unpacking vim-runtime (2:8.2.3995-1ubuntu2.13) ...
Selecting previously unselected package vim.
Preparing to unpack .../vim_2%3a8.2.3995-1ubuntu2.13_amd64.deb ...
Unpacking vim (2:8.2.3995-1ubuntu2.13) ...
Setting up vim-runtime (2:8.2.3995-1ubuntu2.13) ...
Setting up vim (2:8.2.3995-1ubuntu2.13) ...
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/vim (vim) in a                                                                                        uto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/vimdiff (vimdi                                                                                        ff) in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/rvim (rvim) in                                                                                         auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/rview (rview)                                                                                         in auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/vi (vi) in aut                                                                                        o mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/view (view) in                                                                                         auto mode
update-alternatives: using /usr/bin/vim.basic to provide /usr/bin/ex (ex) in aut                                                                                        o mode
Processing triggers for man-db (2.10.2-1) ...
```

`ubuntu@ubuntu-VM:~$ touch my-ns.yaml`
`ubuntu@ubuntu-VM:~$ vim my-ns.yaml`
`ubuntu@ubuntu-VM:~$ cat my-ns.yaml`

```{r}
apiVersion: v1
kind: Namespace
metadata:
  name: <insert-namespace-name-here>
```

`ubuntu@ubuntu-VM:~$ vim my-ns.yaml`
`ubuntu@ubuntu-VM:~$ kubectl create -f my-ns.yaml`

```{r}
namespace/novgems created
```

`ubuntu@ubuntu-VM:~$ kubectl get namespaces`

```{r}
NAME              STATUS   AGE
default           Active   219d
kube-node-lease   Active   219d
kube-public       Active   219d
kube-system       Active   219d
novgems           Active   29s
test              Active   23h
```

`ubuntu@ubuntu-VM:~$ touch nginx-pod.yaml`
`ubuntu@ubuntu-VM:~$ vim nginx-pod`
`ubuntu@ubuntu-VM:~$ cat nginx-pod.yaml`
`ubuntu@ubuntu-VM:~$ vim nginx-pod.yaml`
`ubuntu@ubuntu-VM:~$ cat nginx-pod.yaml`

```{r}
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:

* name: nginx
    image: nginx:1.14.2
    ports:
  * containerPort: 80
```

`ubuntu@ubuntu-VM:~$ vim nginx-pod.yaml`
`ubuntu@ubuntu-VM:~$ vim nginx-pod.yaml`
`ubuntu@ubuntu-VM:~$ nano nginx-pod.yaml`
`ubuntu@ubuntu-VM:~$ cat nginx-pod.yaml`

```{r}
apiVersion: v1
kind: Pod
metadata:
  name: nginxp
spec:
  containers:
* name: nginxc
    image: nginx:1.14.2
    ports:
  * containerPort: 80
```

`ubuntu@ubuntu-VM:~$ kubectl create -f nginx-pod.yaml`

```{r}
pod/nginxp created
```

`ubuntu@ubuntu-VM:~$ kubectl get pods`

```{r}
NAME     READY   STATUS    RESTARTS   AGE
nginxp   1/1     Running   0          20s
```

`ubuntu@ubuntu-VM:~$ mkdir podwithfire`
`ubuntu@ubuntu-VM:~$ ls`

```{r}
Desktop        index.html.12  index.html.19  index.html.25  index.html.31  index.html.38  index.html.44  index.html.6  nginx-pod.yaml  ,ssh
Documents      index.html.13  index.html.2   index.html.26  index.html.32  index.html.39  index.html.45  index.html.7  Pictures        Templates
Downloads      index.html.14  index.html.20  index.html.27  index.html.33  index.html.4   index.html.46  index.html.8  podwithfire     test
index.html     index.html.15  index.html.21  index.html.28  index.html.34  index.html.40  index.html.47  index.html.9  Public          Videos
index.html.1   index.html.16  index.html.22  index.html.29  index.html.35  index.html.41  index.html.48  Music         remoting        workspace
index.html.10  index.html.17  index.html.23  index.html.3   index.html.36  index.html.42  index.html.49  my-ns.yaml    remoting.jar    yaml
index.html.11  index.html.18  index.html.24  index.html.30  index.html.37  index.html.43  index.html.5   nginx-pod     snap
```

`ubuntu@ubuntu-VM:~$ kubectl get pods`

```{r}
NAME     READY   STATUS    RESTARTS   AGE
nginxp   1/1     Running   0          14m
```

`ubuntu@ubuntu-VM:~$ kubectl delete pod nginxp`

```{r}
pod "nginxp" deleted
```

`ubuntu@ubuntu-VM:~$ kubectl get pods`

```{r}
No resources found in default namespace.
```

`ubuntu@ubuntu-VM:~$ touch twocontainer-pod.yaml`
`ubuntu@ubuntu-VM:~$ nano twocontainer-pod.yaml`
`ubuntu@ubuntu-VM:~$ touch twocontainer-pod.yaml`
`ubuntu@ubuntu-VM:~$ cat twocontainer-pod.yaml`

```{r}
apiVersion: v1
kind : Pod
metadata:
  name: twocontainers
spec:
  containers:
* name: simpleservice
    image: nginx:1.14
    ports:
* containerPort: 80
* name: shell
    image: centos
    command:
  * "bin/bash"
  * "-c"
  * "sleep 10000"
```

`ubuntu@ubuntu-VM:~$ kubectl create -f twocontainer-pod.yaml`

```{r}
error: error parsing twocontainer-pod.yaml: error converting YAML to JSON: yaml: line 9: did not find expected key
```

`ubuntu@ubuntu-VM:~$ nano twocontainer-pod.yaml`
`ubuntu@ubuntu-VM:~$ kubectl create -f twocontainer-pod.yaml`
pod/twocontainers created
`ubuntu@ubuntu-VM:~$ kubectl get pods`

```{r}
NAME            READY   STATUS              RESTARTS   AGE
twocontainers   0/2     ContainerCreating   0          17s
```

`ubuntu@ubuntu-VM:~$ kubectl exec -it twocontainers -c simpleservice`

```{r}
error: you must specify at least one command for the container
```

`ubuntu@ubuntu-VM:~$ kubectl exec -it twocontainers -c simpleservice bash`

```{r}
kubectl exec [POD] [COMMAND] is DEPRECATED and will be removed in a future version. Use kubectl exec [POD] -- [COMMAND] instead.
root@twocontainers:/# curl localhost
bash: curl: command not found
root@twocontainers:/# exit
exit
command terminated with exit code 127
```

`ubuntu@ubuntu-VM:~$ kubectl exec -it twocontainers -c shell bin/bash`

`ubuntu@ubuntu-VM:~$ kubectl get namespaces`

```{r}
kubectl exec [POD] [COMMAND] is DEPRECATED and will be removed in a future version. Use kubectl exec [POD] -- [COMMAND] instead.
[root@twocontainers /]# curl localhost
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully instal                                                                                                    led and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
[root@twocontainers /]# exit
exit
```

`ubuntu@ubuntu-VM:~$ kubectl apply -n novegems -f twocontainer-pod.yaml`

```{r}
Error from server (NotFound): error when creating "twocontainer-pod.yaml": namespaces "novegems" not found
```

`ubuntu@ubuntu-VM:~$ kubectl apply -n novgems -f twocontainer-pod.yaml`

```{r}
pod/twocontainers created
```

`ubuntu@ubuntu-VM:~$ kubectl get pods --namespace=novgems`

```{r}
NAME            READY   STATUS    RESTARTS   AGE
twocontainers   2/2     Running   0          31s
```

`ubuntu@ubuntu-VM:~$ kubectl get -o get json pod twocontainers`

```{r}
error: the server doesn't have a resource type "json"
```

`ubuntu@ubuntu-VM:~$ kubectl get -o get yaml pod twocontainers`

```{r}
error: the server doesn't have a resource type "yaml"
```

`ubuntu@ubuntu-VM:~$ kubectl get -o get yaml pod twocontainers --namespace=novgems`

```{r}
error: the server doesn't have a resource type "yaml"
```

`ubuntu@ubuntu-VM:~$ kubectl get -o get pod twocontainers --namespace=novgems`

```{r}
error: unable to match a printer suitable for the output format "get", allowed formats are: custom-columns,custom-columns-file,go-template,go-template-file,json,jsonpath,jsonpath-as-json,jsonpath-file,name,template,templatefile,wide,yaml
```

`ubuntu@ubuntu-VM:~$ kubectl create -f twocontainer-pod.yaml`

```{r}
Error from server (AlreadyExists): error when creating "twocontainer-pod.yaml": pods "twocontainers" already exists
```

`ubuntu@ubuntu-VM:~$ kubectl get pods`

```{r}
NAME            READY   STATUS    RESTARTS   AGE
twocontainers   2/2     Running   0          45m
```


`ubuntu@ubuntu-VM:~$ kubectl get -o json pod twocontainers`

```{r}
{
    "apiVersion": "v1",
    "kind": "Pod",
    "metadata": {
        "creationTimestamp": "2023-11-01T05:56:00Z",
        "name": "twocontainers",
        "namespace": "default",
        "resourceVersion": "129876",
        "uid": "5f0251c4-b7fa-4c91-af6f-9b3db73b1c78"
    },
    "spec": {
        "containers": [
            {
                "image": "nginx:1.14",
                "imagePullPolicy": "IfNotPresent",
                "name": "simpleservice",
                "ports": [
                    {
                        "containerPort": 80,
                        "protocol": "TCP"
                    }
                ],
                "resources": {},
                "terminationMessagePath": "/dev/termination-log",
                "terminationMessagePolicy": "File",
                "volumeMounts": [
                    {
                        "mountPath": "/var/run/secrets/kubernetes.io                                                                                                    /serviceaccount",
                        "name": "kube-api-access-sz524",
                        "readOnly": true
                    }
                ]
            },
            {
                "command": [
                    "bin/bash",
                    "-c",
                    "sleep 10000"
                ],
                "image": "centos",
                "imagePullPolicy": "Always",
                "name": "shell",
                "resources": {},
                "terminationMessagePath": "/dev/termination-log",
                "terminationMessagePolicy": "File",
                "volumeMounts": [
                    {
                        "mountPath": "/var/run/secrets/kubernetes.io                                                                                                    /serviceaccount",
                        "name": "kube-api-access-sz524",
                        "readOnly": true
                    }
                ]
            }
        ],
        "dnsPolicy": "ClusterFirst",
        "enableServiceLinks": true,
        "nodeName": "minikube",
        "preemptionPolicy": "PreemptLowerPriority",
        "priority": 0,
        "restartPolicy": "Always",
        "schedulerName": "default-scheduler",
        "securityContext": {},
        "serviceAccount": "default",
        "serviceAccountName": "default",
        "terminationGracePeriodSeconds": 30,
        "tolerations": [
            {
                "effect": "NoExecute",
                "key": "node.kubernetes.io/not-ready",
                "operator": "Exists",
                "tolerationSeconds": 300
            },
            {
                "effect": "NoExecute",
                "key": "node.kubernetes.io/unreachable",
                "operator": "Exists",
                "tolerationSeconds": 300
            }
        ],
        "volumes": [
            {
                "name": "kube-api-access-sz524",
                "projected": {
                    "defaultMode": 420,
                    "sources": [
                        {
                            "serviceAccountToken": {
                                "expirationSeconds": 3607,
                                "path": "token"
                            }
                        },
                        {
                            "configMap": {
                                "items": [
                                    {
                                        "key": "ca.crt",
                                        "path": "ca.crt"
                                    }
                                ],
                                "name": "kube-root-ca.crt"
                            }
                        },
                        {
                            "downwardAPI": {
                                "items": [
                                    {
                                        "fieldRef": {
                                            "apiVersion": "v1",
                                            "fieldPath": "metadata.namespace"
                                        },
                                        "path": "namespace"
                                    }
                                ]
                            }
                        }
                    ]
                }
            }
        ]
    },
    "status": {
        "conditions": [
            {
                "lastProbeTime": null,
                "lastTransitionTime": "2023-11-01T05:56:00Z",
                "status": "True",
                "type": "Initialized"
            },
            {
                "lastProbeTime": null,
                "lastTransitionTime": "2023-11-01T05:56:19Z",
                "status": "True",
                "type": "Ready"
            },
            {
                "lastProbeTime": null,
                "lastTransitionTime": "2023-11-01T05:56:19Z",
                "status": "True",
                "type": "ContainersReady"
            },
            {
                "lastProbeTime": null,
                "lastTransitionTime": "2023-11-01T05:56:00Z",
                "status": "True",
                "type": "PodScheduled"
            }
        ],
        "containerStatuses": [
            {
                "containerID": "docker://75742bacaee21e868bd88705ff5                                                                                                    9b59be52e6e8848d5173f49c1646801b7d061",
                "image": "centos:latest",
                "imageID": "docker-pullable://centos@sha256:a27fd808                                                                                                    0b517143cbbbab9dfb7c8571c40d67d534bbdee55bd6c473f432b177",
                "lastState": {},
                "name": "shell",
                "ready": true,
                "restartCount": 0,
                "started": true,
                "state": {
                    "running": {
                        "startedAt": "2023-11-01T05:56:18Z"
                    }
                }
            },
            {
                "containerID": "docker://8ac4bdcf719459b5dd77db0f82d                                                                                                    683d2451f60b837bfa1496902636ab291d1b3",
                "image": "nginx:1.14",
                "imageID": "docker-pullable://nginx@sha256:f7988fb6c                                                                                                    02e0ce69257d9bd9cf37ae20a60f1df7563c3a2a6abe24160306b8d",
                "lastState": {},
                "name": "simpleservice",
                "ready": true,
                "restartCount": 0,
                "started": true,
                "state": {
                    "running": {
                        "startedAt": "2023-11-01T05:56:03Z"
                    }
                }
            }
        ],
        "hostIP": "192.168.49.2",
        "phase": "Running",
        "podIP": "172.17.0.3",
        "podIPs": [
            {
                "ip": "172.17.0.3"
            }
        ],
        "qosClass": "BestEffort",
        "startTime": "2023-11-01T05:56:00Z"
    }
}
```

`ubuntu@ubuntu-VM:~$ kubectl get nodes`

```{r}
NAME       STATUS   ROLES                  AGE    VERSION
minikube   Ready    control-plane,master   219d   v1.23.12
```

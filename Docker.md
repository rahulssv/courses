# Docker
## Basic Docker commands
#### Assignment 1

> ubuntu@ubuntu-VM:~$ docker container list

CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
>ubuntu@ubuntu-VM:~$ docker search ubuntu

NAME                             DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
ubuntu                           Ubuntu is a Debian-based Linux operating sys…   16508     [OK]
websphere-liberty                WebSphere Liberty multi-architecture images …   297       [OK]
open-liberty                     Open Liberty multi-architecture images based…   62        [OK]
neurodebian                      NeuroDebian provides neuroscience research s…   105       [OK]
ubuntu-debootstrap               DEPRECATED; use "ubuntu" instead                52        [OK]
ubuntu-upstart                   DEPRECATED, as is Upstart (find other proces…   115       [OK]



>ubuntu@ubuntu-VM:~$ docker search ubuntu/nginx

NAME           DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
ubuntu/nginx   Nginx, a high-performance reverse proxy & we…   102              
>ubuntu@ubuntu-VM:~$ docker search nginx

NAME                               DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
nginx                              Official build of Nginx.                        19145     [OK]

>ubuntu@ubuntu-VM:~$ docker run --help

Usage:  docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

Create and run a new container from an image

Aliases:
  docker container run, docker run

Options:
      --add-host list                  
>ubuntu@ubuntu-VM:~$ docker run -it --name 25octnew pikaso /bin/bash

Unable to find image 'pikaso:latest' locally
docker: Error response from daemon: pull access denied for pikaso, repository does not exist or may require 'docker login': denied: requested access to the resource is denied.
See 'docker run --help'.
>ubuntu@ubuntu-VM:~$ docker build pikaso

[+] Building 0.0s (0/0)
ERROR: unable to prepare context: path "pikaso" not found
ubuntu@ubuntu-VM:~$ docker ps -al
CONTAINER ID   IMAGE     COMMAND       CREATED       STATUS                   PORTS     NAMES
b406446b3169   ubuntu    "/bin/bash"   9 hours ago   Exited (0) 9 hours ago             24octparas
>ubuntu@ubuntu-VM:~$ docker rmi --force b406446b3169

Error response from daemon: No such image: b406446b3169:latest
>ubuntu@ubuntu-VM:~$ docker images

REPOSITORY                  TAG       IMAGE ID       CREATED        SIZE
paraspandey04/24octubuntu   latest    c1f1586671ba   9 hours ago    77.8MB
paraspandey04/23octubuntu   latest    aa26ae99eab8   9 hours ago    77.8MB
ubuntu                      latest    e4c58958181a   2 weeks ago    77.8MB
kicbase/stable              v0.0.37   01c0ce65fff7   9 months ago   1.15GB
>ubuntu@ubuntu-VM:~$ docker rmi --force c1f1586671ba

Untagged: paraspandey04/24octubuntu:latest
Untagged: paraspandey04/24octubuntu@sha256:806789d07b9750f11b5b1e1138a7f740881054f14e7231b55c759415795704b2
Deleted: sha256:c1f1586671ba03d47b2a3e774aa5afa8ea2fe1a6748eaf653d31c959fc217792
Deleted: sha256:ff64dfdf6ce97f06c2006f6f72277f49c6f100794e13f2ecaf6bf486054c4340

>ubuntu@ubuntu-VM:~$ docker images

REPOSITORY                  TAG       IMAGE ID       CREATED        SIZE
paraspandey04/23octubuntu   latest    aa26ae99eab8   9 hours ago    77.8MB
ubuntu                      latest    e4c58958181a   2 weeks ago    77.8MB
kicbase/stable              v0.0.37   01c0ce65fff7   9 months ago   1.15GB

>ubuntu@ubuntu-VM:~$ docker push --help

Usage:  docker push [OPTIONS] NAME[:TAG]

Upload an image to a registry

Aliases:
  docker image push, docker push

Options:
  -a, --all-tags                Push all 
>ubuntu@ubuntu-VM:~$ docker run -it --name 25octparas ubuntu /bin/bash

>root@7a55807663ee:/# ls

bin   dev  home  lib32  libx32  mnt  proc  run   srv  tmp  var
boot  etc  lib   lib64  media   opt  root  sbin  sys  usr

>root@7a55807663ee:/# apt update

Get:1 http://archive.ubuntu.com/ubuntu jammy InRelease [270 kB]
Get:2 http://archive.ubuntu.com/ubuntu jammy-updates InRelease [119 kB]
Get:3 http://archive.ubuntu.com/ubuntu jammy-backports InRelease [109 kB]
Get:4 http://archive.ubuntu.com/ubuntu jammy/universe amd64 Packages [17.5 MB]
Get:5 http://security.ubuntu.com/ubuntu jammy-security InRelease [110 kB]
Get:6 http://security.ubuntu.com/ubuntu jammy-security/restricted amd64 Packages [1305 kB]
Get:7 http://archive.ubuntu.com/ubuntu jammy/restricted amd64 Packages [164 kB]

>root@7a55807663ee:/# echo "hi paras">>25oct23.txt
>root@7a55807663ee:/# hostname

7a55807663ee

>root@7a55807663ee:/# exit
exit

>ubuntu@ubuntu-VM:~$ docker commit 25octparas paraspandey04/25octubuntu

sha256:1d9bde2b7a478bf51806db30732b9cbd43532468dc0e0d77b33c49ebfe307cda
>ubuntu@ubuntu-VM:~$ docker images

REPOSITORY                  TAG       IMAGE ID       CREATED         SIZE
paraspandey04/25octubuntu   latest    1d9bde2b7a47   7 seconds ago   123MB
paraspandey04/23octubuntu   latest    aa26ae99eab8   10 hours ago    77.8MB
ubuntu                      latest    e4c58958181a   2 weeks ago     77.8MB
kicbase/stable              v0.0.37   01c0ce65fff7   9 months ago    1.15GB
>ubuntu@ubuntu-VM:~$ docker login

Authenticating with existing credentials...
WARNING! Your password will be stored unencrypted in /home/ubuntu/.docker/config.json.
Configure a credential helper to remove this warning. See
https://docs.docker.com/engine/reference/commandline/login/#credentials-store

Login Succeeded
>ubuntu@ubuntu-VM:~$ docker push paraspandey04/25octunutu


Using default tag: latest
The push refers to repository [docker.io/paraspandey04/25octunutu]
An image does not exist locally with the tag: paraspandey04/25octunutu
>ubuntu@ubuntu-VM:~$ docker push paraspandey04/25octubuntu

Using default tag: latest
The push refers to repository [docker.io/paraspandey04/25octubuntu]
84b566e7ec57: Pushed
256d88da4185: Mounted from paraspandey04/24octubuntu
latest: digest: sha256:ccb05ca244687455093495d799d4cecff0c29fe9659f887bdeb732dd36379bf0 size: 741

>ubuntu@ubuntu-VM:~$ docker images

REPOSITORY                  TAG       IMAGE ID       CREATED        SIZE
paraspandey04/24octubuntu   latest    c1f1586671ba   9 hours ago    77.8MB
paraspandey04/23octubuntu   latest    aa26ae99eab8   9 hours ago    77.8MB
ubuntu                      latest    e4c58958181a   2 weeks ago    77.8MB
kicbase/stable              v0.0.37   01c0ce65fff7   9 months ago   1.15GB
>ubuntu@ubuntu-VM:~$ docker rmi --force c1f1586671ba

Untagged: paraspandey04/24octubuntu:latest
Untagged: paraspandey04/24octubuntu@sha256:806789d07b9750f11b5b1e1138a7f740881054f14e7231b55c759415795704b2
Deleted: sha256:c1f1586671ba03d47b2a3e774aa5afa8ea2fe1a6748eaf653d31c959fc217792
Deleted: sha256:ff64dfdf6ce97f06c2006f6f72277f49c6f100794e13f2ecaf6bf486054c4340
>ubuntu@ubuntu-VM:~$ docker images

REPOSITORY                  TAG       IMAGE ID       CREATED        SIZE
paraspandey04/23octubuntu   latest    aa26ae99eab8   9 hours ago    77.8MB
ubuntu                      latest    e4c58958181a   2 weeks ago    77.8MB
kicbase/stable              v0.0.37   01c0ce65fff7   9 months ago   1.15GB
>ubuntu@ubuntu-VM:~$ docker push --help

Usage:  docker push [OPTIONS] NAME[:TAG]

#### Assignment 2

>ubuntu@ubuntu-VM:~$ docker images

REPOSITORY                  TAG       IMAGE ID       CREATED          SIZE
paraspandey04/25oct         latest    13b5f42d2dc3   25 minutes ago   77.8MB
paraspandey04/newrepo04     latest    13b5f42d2dc3   25 minutes ago   77.8MB
paraspandey04/25octubuntu   latest    1d9bde2b7a47   2 hours ago      123MB
paraspandey04/23octubuntu   latest    aa26ae99eab8   11 hours ago     77.8MB
ubuntu                      latest    e4c58958181a   2 weeks ago      77.8MB
kicbase/stable              v0.0.37   01c0ce65fff7   9 months ago     1.15GB
ubuntu@ubuntu-VM:~$ docker history --help

Usage:  docker history [OPTIONS] IMAGE

Show the history of an image

Aliases:
  docker image history, docker history

Options:
      --format string   Format output using a custom template:
                        'table':            Print output in table
                        format with column headers (default)
                        'table TEMPLATE':   Print output in table
                        format using the given Go template
                        'json':             Print in JSON format
                        'TEMPLATE':         Print output using
                        the given Go template.
                        Refer to
                        https://docs.docker.com/go/formatting/
                        for more information about formatting
                        output with templates
  -H, --human           Print sizes and dates in human readable
                        format (default true)
      --no-trunc        Don't truncate output
  -q, --quiet           Only show image IDs
ubuntu@ubuntu-VM:~$ docker history  paraspandey04/25octubuntu --format 'json'
{"Comment":"","CreatedAt":"2023-10-25T09:46:05+05:30","CreatedBy":"/bin/bash","CreatedSince":"2 hours ago","ID":"1d9bde2b7a47","Size":"45.2MB"}
{"Comment":"","CreatedAt":"2023-10-05T13:03:32+05:30","CreatedBy":"/bin/sh -c #(nop)  CMD [\"/bin/bash\"]","CreatedSince":"2 weeks ago","ID":"e4c58958181a","Size":"0B"}
{"Comment":"","CreatedAt":"2023-10-05T13:03:32+05:30","CreatedBy":"/bin/sh -c #(nop) ADD file:63d5ab3ef0aab308c…","CreatedSince":"2 weeks ago","ID":"\u003cmissing\u003e","Size":"77.8MB"}
{"Comment":"","CreatedAt":"2023-10-05T13:03:30+05:30","CreatedBy":"/bin/sh -c #(nop)  LABEL org.opencontainers.…","CreatedSince":"2 weeks ago","ID":"\u003cmissing\u003e","Size":"0B"}
{"Comment":"","CreatedAt":"2023-10-05T13:03:30+05:30","CreatedBy":"/bin/sh -c #(nop)  LABEL org.opencontainers.…","CreatedSince":"2 weeks ago","ID":"\u003cmissing\u003e","Size":"0B"}
{"Comment":"","CreatedAt":"2023-10-05T13:03:30+05:30","CreatedBy":"/bin/sh -c #(nop)  ARG LAUNCHPAD_BUILD_ARCH","CreatedSince":"2 weeks ago","ID":"\u003cmissing\u003e","Size":"0B"}
{"Comment":"","CreatedAt":"2023-10-05T13:03:30+05:30","CreatedBy":"/bin/sh -c #(nop)  ARG RELEASE","CreatedSince":"2 weeks ago","ID":"\u003cmissing\u003e","Size":"0B"}
>ubuntu@ubuntu-VM:~$ docker search paraspandey04/25octubuntu

NAME                        DESCRIPTION   STARS     OFFICIAL   AUTOMATED
paraspandey04/25octubuntu                 0
ubuntu@ubuntu-VM:~$ docker inspect --help

Usage:  docker inspect [OPTIONS] NAME|ID [NAME|ID...]

Return low-level information on Docker objects

Options:
  -f, --format string   Format output using a custom template:
                        'json':             Print in JSON format
                        'TEMPLATE':         Print output using
                        the given Go template.
                        Refer to
                        https://docs.docker.com/go/formatting/
                        for more information about formatting
                        output with templates
  -s, --size            Display total file sizes if the type is
                        container
      --type string     Return JSON for specified type
>ubuntu@ubuntu-VM:~$ docker image inspect paraspandey04/25octubuntu

[
    {
        "Id": "sha256:1d9bde2b7a478bf51806db30732b9cbd43532468dc0e0d77b33c49ebfe307cda",
        "RepoTags": [
            "paraspandey04/25octubuntu:latest"
        ],
        "RepoDigests": [
            "paraspandey04/25octubuntu@sha256:ccb05ca244687455093495d799d4cecff0c29fe9659f887bdeb732dd36379bf0"
        ],
        "Parent": "sha256:e4c58958181a5925816faa528ce959e487632f4cfd192f8132f71b32df2744b4",
        "Comment": "",
        "Created": "2023-10-25T04:16:05.84881267Z",
        "Container": "7a55807663eedaab0488847b3adeb128d1b6e091aefbe74e5098c7bc479b9104",
        "ContainerConfig": {
            "Hostname": "7a55807663ee",
            "Domainname": "",
            "User": "",
            "AttachStdin": true,
            "AttachStdout": true,
            "AttachStderr": true,
            "Tty": true,
            "OpenStdin": true,
            "StdinOnce": true,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/bash"
            ],
            "Image": "ubuntu",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {
                "org.opencontainers.image.ref.name": "ubuntu",
                "org.opencontainers.image.version": "22.04"
            }
        },
        "DockerVersion": "23.0.1",
        "Author": "",
        "Config": {
            "Hostname": "7a55807663ee",
            "Domainname": "",
            "User": "",
            "AttachStdin": true,
            "AttachStdout": true,
            "AttachStderr": true,
            "Tty": true,
            "OpenStdin": true,
            "StdinOnce": true,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/bash"
            ],
            "Image": "ubuntu",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {
                "org.opencontainers.image.ref.name": "ubuntu",
                "org.opencontainers.image.version": "22.04"
            }
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 122991619,
        "VirtualSize": 122991619,
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/9f79621309a55b03b4bd403c6d483f54975dbd7452027d8cff9485b9169e7d91/diff",
                "MergedDir": "/var/lib/docker/overlay2/bc779cae4ab14e7449297690d1704482b01106c7bc63c305f399d6a32a98383c/merged",
                "UpperDir": "/var/lib/docker/overlay2/bc779cae4ab14e7449297690d1704482b01106c7bc63c305f399d6a32a98383c/diff",
                "WorkDir": "/var/lib/docker/overlay2/bc779cae4ab14e7449297690d1704482b01106c7bc63c305f399d6a32a98383c/work"
            },
            "Name": "overlay2"
        },
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:256d88da41857db513b95b50ba9a9b28491b58c954e25477d5dad8abb465430b",
                "sha256:84b566e7ec57a167b0fb3fb4efe3ed67fe31c9034776c1a767f5f7959798c649"
            ]
        },
        "Metadata": {
            "LastTagTime": "2023-10-25T09:46:06.05604374+05:30"
        }
    }
]
>ubuntu@ubuntu-VM:~$
pwd
touch dockerfile

=> => sha256:311da6c465ea1576925360eba391bcd32dece9
be9 50.50MB / 50.50MB  0.8s                          => => sha256:ffd9397e94b74abcb54e514f1430e00f604328
d1f 51.89MB / 51.89MB  0.7s                          => => sha256:513d779256048c961239af5f500589330546b0
7 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6[+] Building 77.4s (6/7)                            
                            66fd6192108b67fb57b74753 => => sha256:7e9bf114588c05b2df612b083b96582f3b8dbf
516 17.58MB / 17.58MB  0.3s7d78be1eb92caf6ae84fc3af7 => => sha256:f77a1aef2da8d83e45ec990f45df50f1a286c5
fe8bbfb8c 776B / 776B  0.0se &&     apt-get install  => => sha256:1ddc7e4055fdb6f6bf31063b593befda814294
f9f90 7.23kB / 7.23kB  0.0sOME                       => => sha256:311da6c465ea1576925360eba391bcd32dece9
be9 50.50MB / 50.50MB  0.8s                          => => sha256:ffd9397e94b74abcb54e514f1430e00f604328
d1f 51.89MB / 51.89MB  0.7s                          => => sha256:513d779256048c961239af5f500589330546b0
7 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6[+] Building 77.6s (6/7)                            
                            66fd6192108b67fb57b74753 => => sha256:7e9bf114588c05b2df612b083b96582f3b8dbf
516 17.58MB / 17.58MB  0.3s7d78be1eb92caf6ae84fc3af7 => => sha256:f77a1aef2da8d83e45ec990f45df50f1a286c5
fe8bbfb8c 776B / 776B  0.0se &&     apt-get install  => => sha256:1ddc7e4055fdb6f6bf31063b593befda814294
f9f90 7.23kB / 7.23kB  0.0sOME                       => => sha256:311da6c465ea1576925360eba391bcd32dece9
be9 50.50MB / 50.50MB  0.8s                          => => sha256:ffd9397e94b74abcb54e514f1430e00f604328
d1f 51.89MB / 51.89MB  0.7s                          => => sha256:513d779256048c961239af5f500589330546b0
7 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6[+] Building 77.7s (6/7)                            
                            66fd6192108b67fb57b74753 => => sha256:7e9bf114588c05b2df612b083b96582f3b8dbf
516 17.58MB / 17.58MB  0.3s7d78be1eb92caf6ae84fc3af7 => => sha256:f77a1aef2da8d83e45ec990f45df50f1a286c5
fe8bbfb8c 776B / 776B  0.0se &&     apt-get install  => => sha256:1ddc7e4055fdb6f6bf31063b593befda814294
f9f90 7.23kB / 7.23kB  0.0sOME                       => => sha256:311da6c465ea1576925360eba391bcd32dece9
be9 50.50MB / 50.50MB  0.8s                          => => sha256:ffd9397e94b74abcb54e514f1430e00f604328
d1f 51.89MB / 51.89MB  0.7s                          => => sha256:513d779256048c961239af5f500589330546b0
7 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6[+] Building 77.9s (6/7)                            
                            66fd6192108b67fb57b74753 => => sha256:7e9bf114588c05b2df612b083b96582f3b8dbf
516 17.58MB / 17.58MB  0.3s7d78be1eb92caf6ae84fc3af7 => => sha256:f77a1aef2da8d83e45ec990f45df50f1a286c5
fe8bbfb8c 776B / 776B  0.0se &&     apt-get install  => => sha256:1ddc7e4055fdb6f6bf31063b593befda814294
f9f90 7.23kB / 7.23kB  0.0sOME                       => => sha256:311da6c465ea1576925360eba391bcd32dece9
be9 50.50MB / 50.50MB  0.8s                          => => sha256:ffd9397e94b74abcb54e514f1430e00f604328
d1f 51.89MB / 51.89MB  0.7s                          => => sha256:513d779256048c961239af5f500589330546b0
7 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6[+] Building 78.0s (6/7)                            
                            66fd6192108b67fb57b74753 => => sha256:7e9bf114588c05b2df612b083b96582f3b8dbf
516 17.58MB / 17.58MB  0.3s7d78be1eb92caf6ae84fc3af7 => => sha256:f77a1aef2da8d83e45ec990f45df50f1a286c5
fe8bbfb8c 776B / 776B  0.0se &&     apt-get install  => => sha256:1ddc7e4055fdb6f6bf31063b593befda814294
f9f90 7.23kB / 7.23kB  0.0sOME                       => => sha256:311da6c465ea1576925360eba391bcd32dece9
be9 50.50MB / 50.50MB  0.8s                          => => sha256:ffd9397e94b74abcb54e514f1430e00f604328
d1f 51.89MB / 51.89MB  0.7s                          => => sha256:513d779256048c961239af5f500589330546b0
7 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6[+] Building 78.2s (6/7)                            
                            66fd6192108b67fb57b74753 => => sha256:7e9bf114588c05b2df612b083b96582f3b8dbf
516 17.58MB / 17.58MB  0.3s7d78be1eb92caf6ae84fc3af7 => => sha256:f77a1aef2da8d83e45ec990f45df50f1a286c5
fe8bbfb8c 776B / 776B  0.0se &&     apt-get install  => => sha256:1ddc7e4055fdb6f6bf31063b593befda814294
f9f90 7.23kB / 7.23kB  0.0sOME                       => => sha256:311da6c465ea1576925360eba391bcd32dece9
be9 50.50MB / 50.50MB  0.8s                          => => sha256:ffd9397e94b74abcb54e514f1430e00f604328
d1f 51.89MB / 51.89MB  0.7s                          => => sha256:513d779256048c961239af5f500589330546b0
7 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6[+] Building 78.3s (6/7)                            
                            66fd6192108b67fb57b74753 => => sha256:7e9bf114588c05b2df612b083b96582f3b8dbf
516 17.58MB / 17.58MB  0.3s7d78be1eb92caf6ae84fc3af7 => => sha256:f77a1aef2da8d83e45ec990f45df50f1a286c5
fe8bbfb8c 776B / 776B  0.0se &&     apt-get install  => => sha256:1ddc7e4055fdb6f6bf31063b593befda814294
f9f90 7.23kB / 7.23kB  0.0sOME                       => => sha256:311da6c465ea1576925360eba391bcd32dece9
be9 50.50MB / 50.50MB  0.8s                          => => sha256:ffd9397e94b74abcb54e514f1430e00f604328
d1f 51.89MB / 51.89MB  0.7s                          => => sha256:513d779256048c961239af5f500589330546b0
7 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6[+] Building 78.5s (6/7)                            
                            66fd6192108b67fb57b74753 => => sha256:7e9bf114588c05b2df612b083b96582f3b8dbf
516 17.58MB / 17.58MB  0.3s7d78be1eb92caf6ae84fc3af7 => => sha256:f77a1aef2da8d83e45ec990f45df50f1a286c5
fe8bbfb8c 776B / 776B  0.0se &&     apt-get install  => => sha256:1ddc7e4055fdb6f6bf31063b593befda814294
f9f90 7.23kB / 7.23kB  0.0sOME                       => => sha256:311da6c465ea1576925360eba391bcd32dece9
be9 50.50MB / 50.50MB  0.8s                          => => sha256:ffd9397e94b74abcb54e514f1430e00f604328
d1f 51.89MB / 51.89MB  0.7s                          => => sha256:513d779256048c961239af5f500589330546b0
7 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6[+] Building 78.6s (6/7)                            
                            66fd6192108b67fb57b74753 => => sha256:7e9bf114588c05b2df612b083b96582f3b8dbf
516 17.58MB / 17.58MB  0.3s7d78be1eb92caf6ae84fc3af7 => => sha256:f77a1aef2da8d83e45ec990f45df50f1a286c5
fe8bbfb8c 776B / 776B  0.0se &&     apt-get install  => => sha256:1ddc7e4055fdb6f6bf31063b593befda814294
f9f90 7.23kB / 7.23kB  0.0sOME                       => => sha256:311da6c465ea1576925360eba391bcd32dece9
be9 50.50MB / 50.50MB  0.8s                          => => sha256:ffd9397e94b74abcb54e514f1430e00f604328
d1f 51.89MB / 51.89MB  0.7s                          => => sha256:513d779256048c961239af5f500589330546b0
7 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6[+] Building 78.8s (6/7)                            
                            66fd6192108b67fb57b74753 => => sha256:7e9bf114588c05b2df612b083b96582f3b8dbf
516 17.58MB / 17.58MB  0.3s7d78be1eb92caf6ae84fc3af7 => => sha256:f77a1aef2da8d83e45ec990f45df50f1a286c5
fe8bbfb8c 776B / 776B  0.0se &&     apt-get install  => => sha256:1ddc7e4055fdb6f6bf31063b593befda814294
f9f90 7.23kB / 7.23kB  0.0sOME                       => => sha256:311da6c465ea1576925360eba391bcd32dece9
be9 50.50MB / 50.50MB  0.8s                          => => sha256:ffd9397e94b74abcb54e514f1430e00f604328
d1f 51.89MB / 51.89MB  0.7s                          => => sha256:513d779256048c961239af5f500589330546b0
7 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6[+] Building 78.9s (6/7)                            
                            66fd6192108b67fb57b74753 => => sha256:7e9bf114588c05b2df612b083b96582f3b8dbf
516 17.58MB / 17.58MB  0.3s7d78be1eb92caf6ae84fc3af7 => => sha256:f77a1aef2da8d83e45ec990f45df50f1a286c5
fe8bbfb8c 776B / 776B  0.0se &&     apt-get install  => => sha256:1ddc7e4055fdb6f6bf31063b593befda814294
f9f90 7.23kB / 7.23kB  0.0sOME                       => => sha256:311da6c465ea1576925360eba391bcd32dece9
be9 50.50MB / 50.50MB  0.8s                          => => sha256:ffd9397e94b74abcb54e514f1430e00f604328
d1f 51.89MB / 51.89MB  0.7s                          => => sha256:513d779256048c961239af5f500589330546b0
7 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6[+] Building 79.1s (6/7)                            
                            66fd6192108b67fb57b74753 => => sha256:7e9bf114588c05b2df612b083b96582f3b8dbf
516 17.58MB / 17.58MB  0.3s7d78be1eb92caf6ae84fc3af7 => => sha256:f77a1aef2da8d83e45ec990f45df50f1a286c5
fe8bbfb8c 776B / 776B  0.0se &&     apt-get install  => => sha256:1ddc7e4055fdb6f6bf31063b593befda814294
f9f90 7.23kB / 7.23kB  0.0sOME                       => => sha256:311da6c465ea1576925360eba391bcd32dece9
be9 50.50MB / 50.50MB  0.8s                          => => sha256:ffd9397e94b74abcb54e514f1430e00f604328
d1f 51.89MB / 51.89MB  0.7s                          => => sha256:513d779256048c961239af5f500589330546b0
7 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6[+] Building 79.3s (6/7)                            
                            66fd6192108b67fb57b74753 => => sha256:7e9bf114588c05b2df612b083b96582f3b8dbf
516 17.58MB / 17.58MB  0.3s7d78be1eb92caf6ae84fc3af7 => => sha256:f77a1aef2da8d83e45ec990f45df50f1a286c5
fe8bbfb8c 776B / 776B  0.0se &&     apt-get install  => => sha256:1ddc7e4055fdb6f6bf31063b593befda814294
f9f90 7.23kB / 7.23kB  0.0sOME                       => => sha256:311da6c465ea1576925360eba391bcd32dece9
be9 50.50MB / 50.50MB  0.8s                          => => sha256:ffd9397e94b74abcb54e514f1430e00f604328
d1f 51.89MB / 51.89MB  0.7s                          => => sha256:513d779256048c961239af5f500589330546b0
7 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6[+] Building 79.4s (6/7)                            
                            66fd6192108b67fb57b74753 => => sha256:7e9bf114588c05b2df612b083b96582f3b8dbf
516 17.58MB / 17.58MB  0.3s7d78be1eb92caf6ae84fc3af7 => => sha256:f77a1aef2da8d83e45ec990f45df50f1a286c5
fe8bbfb8c 776B / 776B  0.0se &&     apt-get install  => => sha256:1ddc7e4055fdb6f6bf31063b593befda814294
f9f90 7.23kB / 7.23kB  0.0sOME                       => => sha256:311da6c465ea1576925360eba391bcd32dece9
be9 50.50MB / 50.50MB  0.8s                          => => sha256:ffd9397e94b74abcb54e514f1430e00f604328
d1f 51.89MB / 51.89MB  0.7s                          => => sha256:513d779256048c961239af5f500589330546b0
7 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6[+] Building 79.6s (6/7)                            
                            66fd6192108b67fb57b74753 => => sha256:7e9bf114588c05b2df612b083b96582f3b8dbf
516 17.58MB / 17.58MB  0.3s7d78be1eb92caf6ae84fc3af7 => => sha256:f77a1aef2da8d83e45ec990f45df50f1a286c5
fe8bbfb8c 776B / 776B  0.0se &&     apt-get install  => => sha256:1ddc7e4055fdb6f6bf31063b593befda814294
f9f90 7.23kB / 7.23kB  0.0sOME                       => => sha256:311da6c465ea1576925360eba391bcd32dece9
be9 50.50MB / 50.50MB  0.8s                          => => sha256:ffd9397e94b74abcb54e514f1430e00f604328
d1f 51.89MB / 51.89MB  0.7s                          => => sha256:513d779256048c961239af5f500589330546b0
7 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6[+] Building 79.7s (6/7)                            
                            66fd6192108b67fb57b74753 => => sha256:7e9bf114588c05b2df612b083b96582f3b8dbf
516 17.58MB / 17.58MB  0.3s7d78be1eb92caf6ae84fc3af7 => => sha256:f77a1aef2da8d83e45ec990f45df50f1a286c5
fe8bbfb8c 776B / 776B  0.0se &&     apt-get install  => => sha256:1ddc7e4055fdb6f6bf31063b593befda814294
f9f90 7.23kB / 7.23kB  0.0sOME                       => => sha256:311da6c465ea1576925360eba391bcd32dece9
be9 50.50MB / 50.50MB  0.8s                          => => sha256:ffd9397e94b74abcb54e514f1430e00f604328
d1f 51.89MB / 51.89MB  0.7s                          => => sha256:513d779256048c961239af5f500589330546b0
7 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6[+] Building 79.9s (6/7)                            
                            66fd6192108b67fb57b74753 => => sha256:7e9bf114588c05b2df612b083b96582f3b8dbf
516 17.58MB / 17.58MB  0.3s7d78be1eb92caf6ae84fc3af7 => => sha256:f77a1aef2da8d83e45ec990f45df50f1a286c5
fe8bbfb8c 776B / 776B  0.0se &&     apt-get install  => => sha256:1ddc7e4055fdb6f6bf31063b593befda814294
f9f90 7.23kB / 7.23kB  0.0sOME                       => => sha256:311da6c465ea1576925360eba391bcd32dece9
be9 50.50MB / 50.50MB  0.8s                          => => sha256:ffd9397e94b74abcb54e514f1430e00f604328
d1f 51.89MB / 51.89MB  0.7s                          => => sha256:513d779256048c961239af5f500589330546b0
7 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6[+] Building 80.0s (6/7)                            
                            66fd6192108b67fb57b74753 => => sha256:7e9bf114588c05b2df612b083b96582f3b8dbf
516 17.58MB / 17.58MB  0.3s7d78be1eb92caf6ae84fc3af7 => => sha256:f77a1aef2da8d83e45ec990f45df50f1a286c5
fe8bbfb8c 776B / 776B  0.0se &&     apt-get install  => => sha256:1ddc7e4055fdb6f6bf31063b593befda814294
f9f90 7.23kB / 7.23kB  0.0sOME                       => => sha256:311da6c465ea1576925360eba391bcd32dece9
be9 50.50MB / 50.50MB  0.8s                          => => sha256:ffd9397e94b74abcb54e514f1430e00f604328
d1f 51.89MB / 51.89MB  0.7s                          => => sha256:513d779256048c961239af5f500589330546b0
7 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6[+] Building 80.2s (6/7)                            
                            66fd6192108b67fb57b74753 => => sha256:7e9bf114588c05b2df612b083b96582f3b8dbf
516 17.58MB / 17.58MB  0.3s7d78be1eb92caf6ae84fc3af7 => => sha256:f77a1aef2da8d83e45ec990f45df50f1a286c5
fe8bbfb8c 776B / 776B  0.0se &&     apt-get install  => => sha256:1ddc7e4055fdb6f6bf31063b593befda814294
f9f90 7.23kB / 7.23kB  0.0sOME                       => => sha256:311da6c465ea1576925360eba391bcd32dece9
be9 50.50MB / 50.50MB  0.8s                          => => sha256:ffd9397e94b74abcb54e514f1430e00f604328
d1f 51.89MB / 51.89MB  0.7s                          => => sha256:513d779256048c961239af5f500589330546b0
7 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6[+] Building 80.3s (6/7)                            
                            66fd6192108b67fb57b74753 => => sha256:7e9bf114588c05b2df612b083b96582f3b8dbf
516 17.58MB / 17.58MB  0.3s7d78be1eb92caf6ae84fc3af7 => => sha256:f77a1aef2da8d83e45ec990f45df50f1a286c5
fe8bbfb8c 776B / 776B  0.0se &&     apt-get install  => => sha256:1ddc7e4055fdb6f6bf31063b593befda814294
f9f90 7.23kB / 7.23kB  0.0sOME                       => => sha256:311da6c465ea1576925360eba391bcd32dece9
be9 50.50MB / 50.50MB  0.8s                          => => sha256:ffd9397e94b74abcb54e514f1430e00f604328
d1f 51.89MB / 51.89MB  0.7s                          => => sha256:513d779256048c961239af5f500589330546b0
7 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6[+] Building 80.5s (6/7)                            
                            66fd6192108b67fb57b74753 => => sha256:7e9bf114588c05b2df612b083b96582f3b8dbf
516 17.58MB / 17.58MB  0.3s7d78be1eb92caf6ae84fc3af7 => => sha256:f77a1aef2da8d83e45ec990f45df50f1a286c5
fe8bbfb8c 776B / 776B  0.0se &&     apt-get install  => => sha256:1ddc7e4055fdb6f6bf31063b593befda814294
f9f90 7.23kB / 7.23kB  0.0sOME                       => => sha256:311da6c465ea1576925360eba391bcd32dece9
be9 50.50MB / 50.50MB  0.8s                          => => sha256:ffd9397e94b74abcb54e514f1430e00f604328
d1f 51.89MB / 51.89MB  0.7s                          => => sha256:513d779256048c961239af5f500589330546b0
7 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6[+] Building 80.6s (6/7)                            
                            66fd6192108b67fb57b74753 => => sha256:7e9bf114588c05b2df612b083b96582f3b8dbf
516 17.58MB / 17.58MB  0.3s7d78be1eb92caf6ae84fc3af7 => => sha256:f77a1aef2da8d83e45ec990f45df50f1a286c5
fe8bbfb8c 776B / 776B  0.0se &&     apt-get install  => => sha256:1ddc7e4055fdb6f6bf31063b593befda814294
f9f90 7.23kB / 7.23kB  0.0sOME                       => => sha256:311da6c465ea1576925360eba391bcd32dece9
be9 50.50MB / 50.50MB  0.8s                          => => sha256:ffd9397e94b74abcb54e514f1430e00f604328
d1f 51.89MB / 51.89MB  0.7s                          => => sha256:513d779256048c961239af5f500589330546b0
7 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6[+] Building 80.8s (6/7)                            
                            66fd6192108b67fb57b74753 => => sha256:7e9bf114588c05b2df612b083b96582f3b8dbf
516 17.58MB / 17.58MB  0.3s7d78be1eb92caf6ae84fc3af7 => => sha256:f77a1aef2da8d83e45ec990f45df50f1a286c5
fe8bbfb8c 776B / 776B  0.0se &&     apt-get install  => => sha256:1ddc7e4055fdb6f6bf31063b593befda814294
f9f90 7.23kB / 7.23kB  0.0sOME                       => => sha256:311da6c465ea1576925360eba391bcd32dece9
be9 50.50MB / 50.50MB  0.8s                          => => sha256:ffd9397e94b74abcb54e514f1430e00f604328
d1f 51.89MB / 51.89MB  0.7s                          => => sha256:513d779256048c961239af5f500589330546b0
7 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6[+] Building 80.9s (6/7)                            
                            66fd6192108b67fb57b74753 => => sha256:7e9bf114588c05b2df612b083b96582f3b8dbf
516 17.58MB / 17.58MB  0.3s7d78be1eb92caf6ae84fc3af7 => => sha256:f77a1aef2da8d83e45ec990f45df50f1a286c5
fe8bbfb8c 776B / 776B  0.0se &&     apt-get install  => => sha256:1ddc7e4055fdb6f6bf31063b593befda814294
f9f90 7.23kB / 7.23kB  0.0sOME                       => => sha256:311da6c465ea1576925360eba391bcd32dece9
be9 50.50MB / 50.50MB  0.8s                          => => sha256:ffd9397e94b74abcb54e514f1430e00f604328
d1f 51.89MB / 51.89MB  0.7s                          => => sha256:513d779256048c961239af5f500589330546b0
7 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6[+] Building 81.1s (6/7)                            
                            66fd6192108b67fb57b74753 => => sha256:7e9bf114588c05b2df612b083b96582f3b8dbf
516 17.58MB / 17.58MB  0.3s7d78be1eb92caf6ae84fc3af7 => => sha256:f77a1aef2da8d83e45ec990f45df50f1a286c5
fe8bbfb8c 776B / 776B  0.0se &&     apt-get install  => => sha256:1ddc7e4055fdb6f6bf31063b593befda814294
f9f90 7.23kB / 7.23kB  0.0sOME                       => => sha256:311da6c465ea1576925360eba391bcd32dece9
be9 50.50MB / 50.50MB  0.8s                          => => sha256:ffd9397e94b74abcb54e514f1430e00f604328
d1f 51.89MB / 51.89MB  0.7s                          => => sha256:513d779256048c961239af5f500589330546b0
7 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6[+] Building 81.2s (6/7)                            
                            66fd6192108b67fb57b74753 => => sha256:7e9bf114588c05b2df612b083b96582f3b8dbf
516 17.58MB / 17.58MB  0.3s7d78be1eb92caf6ae84fc3af7 => => sha256:f77a1aef2da8d83e45ec990f45df50f1a286c5
fe8bbfb8c 776B / 776B  0.0se &&     apt-get install  => => sha256:1ddc7e4055fdb6f6bf31063b593befda814294
f9f90 7.23kB / 7.23kB  0.0sOME                       => => sha256:311da6c465ea1576925360eba391bcd32dece9
be9 50.50MB / 50.50MB  0.8s                          => => sha256:ffd9397e94b74abcb54e514f1430e00f604328
d1f 51.89MB / 51.89MB  0.7s                          => => sha256:513d779256048c961239af5f500589330546b0
7 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6[+] Building 81.3s (6/7)                            
                            66fd6192108b67fb57b74753 => => sha256:7e9bf114588c05b2df612b083b96582f3b8dbf
516 17.58MB / 17.58MB  0.3s7d78be1eb92caf6ae84fc3af7 => => sha256:f77a1aef2da8d83e45ec990f45df50f1a286c5
fe8bbfb8c 776B / 776B  0.0se &&     apt-get install  => => sha256:1ddc7e4055fdb6f6bf31063b593befda814294
f9f90 7.23kB / 7.23kB  0.0sOME                       => => sha256:311da6c465ea1576925360eba391bcd32dece9
be9 50.50MB / 50.50MB  0.8s                          => => sha256:ffd9397e94b74abcb54e514f1430e00f604328
d1f 51.89MB / 51.89MB  0.7s                          => => sha256:513d779256048c961239af5f500589330546b0
7 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6[+] Building 81.4s (7/7) FINISHED                   
                            66fd6192108b67fb57b74753 => [internal] load build definition from dockerfile
                       0.0s7d78be1eb92caf6ae84fc3af7 => => transferring dockerfile: 295B                
                       0.0se &&     apt-get install  => [internal] load .dockerignore                   
                       0.0sOME                       => => transferring context: 2B                     
                       0.0s                          => [internal] load metadata for docker.io/library/n
ode:16                 0.4s                          => [1/3] FROM docker.io/library/node:16@sha256:f77a
1aef2da8d83e45ec990f  33.0s
 => => resolve docker.io/library/node:16@sha256:f77a1aef2da8d83e45ec990f4  0.0s
 => => sha256:c94b82f9827cab6e421b350965a9ef11b25b13ffbd1 2.00kB / 2.00kB  0.0s
 => => sha256:7e9bf114588c05b2df612b083b96582f3b8dbf516 17.58MB / 17.58MB  0.3s
 => => sha256:f77a1aef2da8d83e45ec990f45df50f1a286c5fe8bbfb8c 776B / 776B  0.0s
 => => sha256:1ddc7e4055fdb6f6bf31063b593befda814294f9f90 7.23kB / 7.23kB  0.0s
 => => sha256:311da6c465ea1576925360eba391bcd32dece9be9 50.50MB / 50.50MB  0.8s
 => => sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f 51.89MB / 51.89MB  0.7s
 => => sha256:513d779256048c961239af5f500589330546b07 191.90MB / 191.90MB  2.8s
 => => sha256:0e421f66aff42bb069dffc26af6d132194b22a108 34.79MB / 34.79MB  1.3s
 => => sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae 4.20kB / 4.20kB  0.8s
 => => sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458ba 2.27MB / 2.27MB  1.0s
 => => extracting sha256:311da6c465ea1576925360eba391bcd32dece9be95960a0b  5.8s
 => => sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967 450B / 450B  1.0s
 => => extracting sha256:7e9bf114588c05b2df612b083b96582f3b8dbf51647aa613  1.1s
 => => extracting sha256:ffd9397e94b74abcb54e514f1430e00f604328d1f895eadb  5.2s
 => => extracting sha256:513d779256048c961239af5f500589330546b0727752172  15.8s
 => => extracting sha256:ae3b95bbaa61ce24cefdd89e7c74d6fbd7713b2bcae93af4  0.0s
 => => extracting sha256:0e421f66aff42bb069dffc26af6d132194b22a1082b08c5e  2.9s
 => => extracting sha256:ca266fd6192108b67fb57b74753a8c4ca5d8bd458baae3d4  0.2s
 => => extracting sha256:ee7d78be1eb92caf6ae84fc3af736b23eca018d5dedc967a  0.0s
 => [2/3] RUN apt-get update &&     apt-get install -y openjdk-11-jdk ca  41.4s
 => [3/3] RUN export JAVA_HOME                                             0.9s
 => exporting to image                                                     5.5s
 => => exporting layers                                                    5.5s
 => => writing image sha256:baea0d3998060a89bdd61431b4a973685c64d5f69f11f  0.0s
 => => naming to docker.io/library/javaimage                               0.0s
[node2] (local) root@192.168.0.7 ~
$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED          SIZE
javaimage    latest    baea0d399806   14 seconds ago   1.43GB
[node2] (local) root@192.168.0.7 ~
$ docker run -p 8080:8080 javaimage
openjdk version "11.0.20" 2023-07-18
OpenJDK Runtime Environment (build 11.0.20+8-post-Debian-1deb10u1)
OpenJDK 64-Bit Server VM (build 11.0.20+8-post-Debian-1deb10u1, mixed mode, sharing)
[node2] (local) root@192.168.0.7 ~
$ ls
dockerfile
[node2] (local) root@192.168.0.7 ~
$ cd dockerfile
bash: cd: dockerfile: Not a directory
[node2] (local) root@192.168.0.7 ~
$ cat dockerfile
FROM node:16
RUN apt-get update && \
    apt-get install -y openjdk-11-jdk ca-certificates-java && \
    apt-get clean && \
    update-ca-certificates -f
ENV JAVA_HOME /usr/lib/jvm/java-11-openjdk-amd64/
RUN export JAVA_HOME
CMD ["java", "-version"][node2] (local) root@192.168.0.7 ~
$ 
[node2] (local) root@192.168.0.7 ~
$ ^C
[node2] (local) root@192.168.0.7 ~
$ ###############################################################
[node1] (local) root@192.168.0.18 ~
$ docker volume create myvol2
myvol2
[node1] (local) root@192.168.0.18 ~
$ docker run -it \
>  --name devtest\
>  -v myvol2:/app\
>  ubuntu /bin/bash
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
aece8493d397: Pull complete 
Digest: sha256:2b7412e6465c3c7fc5bb21d3e6f1917c167358449fecac8176c6e496e5c1f05f
Status: Downloaded newer image for ubuntu:latest
root@998b971112e9:/# echo "hello">>paras.txt
root@998b971112e9:/# ls
app   dev   lib    libx32  opt        root  srv  usr
bin   etc   lib32  media   paras.txt  run   sys  var
boot  home  lib64  mnt     proc       sbin  tmp
root@998b971112e9:/# cat paras.txt
hello
root@998b971112e9:/# exit
exit
[node1] (local) root@192.168.0.18 ~
$ docker volume inspect myvol2
[
    {
        "CreatedAt": "2023-10-26T03:47:44Z",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/myvol2/_data",
        "Name": "myvol2",
        "Options": null,
        "Scope": "local"
    }
]
[node1] (local) root@192.168.0.18 ~
$ [node1] (local) root@192.168.0.18 ~
$ docker volume create myvol2
myvol2
[node1] (local) root@192.168.0.18 ~
$ docker run -it \
>  --name devtest\
>  -v myvol2:/app\
>  ubuntu /bin/bash
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
aece8493d397: Pull complete 
Digest: sha256:2b7412e6465c3c7fc5bb21d3e6f1917c167358449fecac8176c6e496e5c1f05f
Status: Downloaded newer image for ubuntu:latest
root@998b971112e9:/# echo "hello">>paras.txt
root@998b971112e9:/# ls
app   dev   lib    libx32  opt        root  srv  usr
bin   etc   lib32  media   paras.txt  run   sys  var
boot  home  lib64  mnt     proc       sbin  tmp
root@998b971112e9:/# cat paras.txt
hello
root@998b971112e9:/# exit
exit
[node1] (local) root@192.168.0.18 ~
$ docker volume inspect myvol2
[
    {
        "CreatedAt": "2023-10-26T03:47:44Z",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/myvol2/_data",
        "Name": "myvol2",
        "Options": null,
        "Scope": "local"
    }
]
[node1] (local) root@192.168.0.18 ~
$ mkdir /onhost
[node1] (local) root@192.168.0.18 ~
$ exit
logout
###############################################################
#                          WARNING!!!!                        #
# This is a sandbox environment. Using personal credentials   #
# is HIGHLY! discouraged. Any consequences of doing so are    #
# completely the user's responsibilites.                      #
#                                                             #
# The PWD team.                                               #
###############################################################
[node1] (local) root@192.168.0.18 ~
$ docker container run -d -p 3306:3306 --name mydb -v ~/sqldata:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=pass mysql
Unable to find image 'mysql:latest' locally
latest: Pulling from library/mysql
8e0176adc18c: Pull complete 
14e977b0f4b2: Pull complete 
a7b58dd6f78b: Pull complete 
fba70cc872a5: Pull complete 
5db2cc6eab8f: Pull complete 
081f41f573ba: Pull complete 
86bf2dc4ded9: Pull complete 
47f08b0e916e: Pull complete 
850e29ae8eeb: Pull complete 
13517fe0d921: Pull complete 
Digest: sha256:f61944ff3f2961363a4d22913b2ac581523273679d7e14dd26e8db8c9f571a7e
Status: Downloaded newer image for mysql:latest
b4d5c3bf3231421fe700543a09e3ae2acd9e67fe0f85b841a20c2c8bf3c81b0c
[node1] (local) root@192.168.0.18 ~
$ ls ~/sqldata
#ib_16384_0.dblwr   ca.pem              performance_schema
#ib_16384_1.dblwr   client-cert.pem     private_key.pem
#innodb_redo        client-key.pem      public_key.pem
#innodb_temp        ib_buffer_pool      server-cert.pem
auto.cnf            ibdata1             server-key.pem
binlog.000001       ibtmp1              sys
binlog.000002       mysql               undo_001
binlog.index        mysql.ibd           undo_002
ca-key.pem          mysql.sock
[node1] (local) root@192.168.0.18 ~
$ [node1] (local) root@192.168.0.18 ~
$ docker volume create myvol2
myvol2
[node1] (local) root@192.168.0.18 ~
$ docker run -it \
>  --name devtest\
>  -v myvol2:/app\
>  ubuntu /bin/bash
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
aece8493d397: Pull complete 
Digest: sha256:2b7412e6465c3c7fc5bb21d3e6f1917c167358449fecac8176c6e496e5c1f05f
Status: Downloaded newer image for ubuntu:latest
root@998b971112e9:/# echo "hello">>paras.txt
root@998b971112e9:/# ls
app   dev   lib    libx32  opt        root  srv  usr
bin   etc   lib32  media   paras.txt  run   sys  var
boot  home  lib64  mnt     proc       sbin  tmp
root@998b971112e9:/# cat paras.txt
hello
root@998b971112e9:/# exit
exit
[node1] (local) root@192.168.0.18 ~
$ docker volume inspect myvol2
[
    {
        "CreatedAt": "2023-10-26T03:47:44Z",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/myvol2/_data",
        "Name": "myvol2",
        "Options": null,
        "Scope": "local"
    }
]
[node1] (local) root@192.168.0.18 ~
$ mkdir /onhost
[node1] (local) root@192.168.0.18 ~
$ exit
logout
###############################################################
#                          WARNING!!!!                        #
# This is a sandbox environment. Using personal credentials   #
# is HIGHLY! discouraged. Any consequences of doing so are    #
# completely the user's responsibilites.                      #
#                                                             #
# The PWD team.                                               #
###############################################################
[node1] (local) root@192.168.0.18 ~
$ docker container run -d -p 3306:3306 --name mydb -v ~/sqldata:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=pass mysql
Unable to find image 'mysql:latest' locally
latest: Pulling from library/mysql
8e0176adc18c: Pull complete 
14e977b0f4b2: Pull complete 
a7b58dd6f78b: Pull complete 
fba70cc872a5: Pull complete 
5db2cc6eab8f: Pull complete 
081f41f573ba: Pull complete 
86bf2dc4ded9: Pull complete 
47f08b0e916e: Pull complete 
850e29ae8eeb: Pull complete 
13517fe0d921: Pull complete 
Digest: sha256:f61944ff3f2961363a4d22913b2ac581523273679d7e14dd26e8db8c9f571a7e
Status: Downloaded newer image for mysql:latest
b4d5c3bf3231421fe700543a09e3ae2acd9e67fe0f85b841a20c2c8bf3c81b0c
[node1] (local) root@192.168.0.18 ~
$ ls ~/sqldata
#ib_16384_0.dblwr   ca.pem              performance_schema
#ib_16384_1.dblwr   client-cert.pem     private_key.pem
#innodb_redo        client-key.pem      public_key.pem
#innodb_temp        ib_buffer_pool      server-cert.pem
auto.cnf            ibdata1             server-key.pem
binlog.000001       ibtmp1              sys
binlog.000002       mysql               undo_001
binlog.index        mysql.ibd           undo_002
ca-key.pem          mysql.sock
[node1] (local) root@192.168.0.18 ~
$ [node1] (local) root@192.168.0.18 ~
$ docker volume create myvol2
myvol2
[node1] (local) root@192.168.0.18 ~
$ docker run -it \
>  --name devtest\
>  -v myvol2:/app\
>  ubuntu /bin/bash
Unable to find image 'ubuntu:latest' locally
latest: Pulling from library/ubuntu
aece8493d397: Pull complete 
Digest: sha256:2b7412e6465c3c7fc5bb21d3e6f1917c167358449fecac8176c6e496e5c1f05f
Status: Downloaded newer image for ubuntu:latest
root@998b971112e9:/# echo "hello">>paras.txt
root@998b971112e9:/# ls
app   dev   lib    libx32  opt        root  srv  usr
bin   etc   lib32  media   paras.txt  run   sys  var
boot  home  lib64  mnt     proc       sbin  tmp
root@998b971112e9:/# cat paras.txt
hello
root@998b971112e9:/# exit
exit
[node1] (local) root@192.168.0.18 ~
$ docker volume inspect myvol2
[
    {
        "CreatedAt": "2023-10-26T03:47:44Z",
        "Driver": "local",
        "Labels": null,
        "Mountpoint": "/var/lib/docker/volumes/myvol2/_data",
        "Name": "myvol2",
        "Options": null,
        "Scope": "local"
    }
]
[node1] (local) root@192.168.0.18 ~
$ mkdir /onhost
[node1] (local) root@192.168.0.18 ~
$ exit
logout
###############################################################
#                          WARNING!!!!                        #
# This is a sandbox environment. Using personal credentials   #
# is HIGHLY! discouraged. Any consequences of doing so are    #
# completely the user's responsibilites.                      #
#                                                             #
# The PWD team.                                               #
###############################################################
[node1] (local) root@192.168.0.18 ~
$ docker container run -d -p 3306:3306 --name mydb -v ~/sqldata:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=pass mysql
Unable to find image 'mysql:latest' locally
latest: Pulling from library/mysql
8e0176adc18c: Pull complete 
14e977b0f4b2: Pull complete 
a7b58dd6f78b: Pull complete 
fba70cc872a5: Pull complete 
5db2cc6eab8f: Pull complete 
081f41f573ba: Pull complete 
86bf2dc4ded9: Pull complete 
47f08b0e916e: Pull complete 
850e29ae8eeb: Pull complete 
13517fe0d921: Pull complete 
Digest: sha256:f61944ff3f2961363a4d22913b2ac581523273679d7e14dd26e8db8c9f571a7e
Status: Downloaded newer image for mysql:latest
b4d5c3bf3231421fe700543a09e3ae2acd9e67fe0f85b841a20c2c8bf3c81b0c
[node1] (local) root@192.168.0.18 ~
$ ls ~/sqldata
#ib_16384_0.dblwr   ca.pem              performance_schema
#ib_16384_1.dblwr   client-cert.pem     private_key.pem
#innodb_redo        client-key.pem      public_key.pem
#innodb_temp        ib_buffer_pool      server-cert.pem
auto.cnf            ibdata1             server-key.pem
binlog.000001       ibtmp1              sys
binlog.000002       mysql               undo_001
binlog.index        mysql.ibd           undo_002
ca-key.pem          mysql.sock
[node1] (local) root@192.168.0.18 ~
$ 

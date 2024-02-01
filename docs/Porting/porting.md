# Porting Open Source Packages to Linux on Power
### To install docker on linux ppc64le 
## Setup
```sh
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh ./get-docker.sh --dry-run

sudo chmod 666 /var/run/docker.sock

```
### Pull the base image. ​
```sh
 docker pull registry.access.redhat.com/ubi8/ubi:8.4​
```
### Create container. ​
```sh
docker run -it --name cordova-plugin-firebase registry.access.redhat.com/ubi8/ubi:8.4 /bin/bash​

```
## Porting
### loopback-connector
```sh
#!/bin/bash -e

PACKAGE_NAME=loopback-connector
PACKAGE_URL=https://github.com/loopbackio/loopback-connector

export NODE_VERSION=${NODE_VERSION:-16}
yum install -y python38 python38-devel git gcc gcc-c++ libffi make

#Installing nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
source "$HOME"/.bashrc
echo "installing nodejs $NODE_VERSION"
nvm install "$NODE_VERSION" >/dev/null
nvm use $NODE_VERSION



git clone $PACKAGE_URL $PACKAGE_NAME
cd  $PACKAGE_NAME

npm install && npm audit fix --force > loopback_install.log
npm test > loopback_test.log

```
### markdown
```sh
#!/bin/bash -e

set -e


# Variables
export PACKAGE_NAME=markdown
export PACKAGE_URL=https://github.com/Python-Markdown/markdown

# Install dependencies
yum install -y wget gcc git gcc-c++
yum install -y python38-devel.ppc64le
python3 -m pip install build tox coverage codecov

# Clone the repository
git clone $PACKAGE_URL
cd $PACKAGE_NAME

python3 -m build > markdown_build.log
python3 -m tox -e py3 > markdown_test.log

```
### onnxruntime
```sh
#!/bin/bash -e

PACKAGE_NAME=onnxruntime
PACKAGE_VERSION=1.10.0
PACKAGE_URL=https://github.com/microsoft/onnxruntime.git

set -e
yum install -y python3 git cmake gcc-c++ java-1.8.0-openjdk-devel
cd /home

git clone $PACKAGE_URL
cd $PACKAGE_NAME
git checkout v$PACKAGE_VERSION
./build.sh > onnxruntime_build.log

exit 0

```
### passport
```sh
#!/bin/bash -e

PACKAGE_NAME=passport
PACKAGE_URL=https://github.com/jaredhanson/passport.git

export NODE_VERSION=${NODE_VERSION:-16}
yum install -y python38 python38-devel git gcc gcc-c++ libffi make

#Installing nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
source "$HOME"/.bashrc
echo "installing nodejs $NODE_VERSION"
nvm install "$NODE_VERSION" >/dev/null
nvm use $NODE_VERSION



git clone $PACKAGE_URL
cd  $PACKAGE_NAME

npm install && npm audit fix --force > passport_install.log
npm test > passport_test.log

```
###  strftime
```sh
#!/bin/bash -e

PACKAGE_NAME=strftime
PACKAGE_URL=https://github.com/samsonjs/strftime/

export NODE_VERSION=${NODE_VERSION:-16}
yum install git make -y

#Installing nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
source "$HOME"/.bashrc
echo "installing nodejs $NODE_VERSION"
nvm install "$NODE_VERSION" >/dev/null
nvm use $NODE_VERSION

git clone $PACKAGE_URL $PACKAGE_NAME
cd  $PACKAGE_NAME

npm install && npm audit fix --force > strftime_install.log
make test > strftime_test.log

```
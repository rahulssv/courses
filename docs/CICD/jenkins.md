# CICD with Jenkins
## Jenkins container with oc and docker installed
- First download oc cli tar file in root folder.
- [Install OC client in Ubuntu/Debian](https://gist.github.com/mehdihasan/3399998cba54bdec78deb9be4a002acb)
```Dockerfile
FROM docker.io/jenkins/jenkins:lts
USER root
COPY $PWD/oc /usr/local/bin/
RUN chmod +x /usr/local/bin/oc
RUN apt-get update -qq \
    && apt-get install -qqy apt-transport-https ca-certificates curl gnupg2 software-properties-common 
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"
RUN apt-get update  -qq \
    && apt-cache policy docker-ce\
    && apt-get install docker-ce -y
RUN usermod -aG docker jenkins
```
- `docker build -t rahul1181/jenkins .`
- `chown 1000 $PWD/jenkins`
- `cd jenkins/`
- `docker run -d -p 49001:8080 -v /var/run/docker.sock:/var/run/docker.sock -v $PWD/jenkins:/var/jenkins_home:z -t rahul1181/jenkins`


## Setup user and Install plugins
### plugins
- pipeline
- git
- docker : pipeline, 
- openshift
- credentials

## Setup Credentials
- DOCKER_ID: username, password
- OPENSHIFT_ID: secret(token)
- GITHUB_LOGIN: username, password

## Create a pipeline (jttours)
- Add the git repository url.
- Place Jenkinsfile in root of git repository.

`Jenkinsfile`
```groovy 
pipeline {
    agent any
 
    environment {
        OPENSHIFT_SERVER = 'https://c100-e.us-south.containers.cloud.ibm.com:30954'
        OPENSHIFT_PROJECT = 'jttours'
        OPENSHIFT_TOKEN_CREDENTIALS_ID = 'OPENSHIFT_ID'
        DOCKER_HUB_CREDENTIALS = 'DOCKER_ID'
        FRONTEND_IMAGE_NAME = 'rahul1181/frontend-image:1.16'
        BACKEND_IMAGE_NAME = 'rahul1181/backend-image:1.3'
    }
 
    stages {
        stage('Authenticate to OpenShift') {
            steps {
                script {
                    withCredentials([string(credentialsId: OPENSHIFT_TOKEN_CREDENTIALS_ID, variable: 'OPENSHIFT_TOKEN')]) {
                        sh "oc login --token=${OPENSHIFT_TOKEN} ${OPENSHIFT_SERVER}"
                    }
                }
            }
        }
        stage('Build and Push Images') {
            parallel {
                stage('Frontend') {
                    steps {
                        script {
                            // Build frontend Docker image
                            sh "docker build -t ${FRONTEND_IMAGE_NAME} ./frontend"
                            // Push frontend image to Docker Hub
                            dockerLoginAndPush(FRONTEND_IMAGE_NAME)
                        }
                    }
                }
                stage('Backend') {
                    steps {
                        script {
                            // Build backend Docker image
                            sh "docker build -t ${BACKEND_IMAGE_NAME} ./backend"
                            // Push backend image to Docker Hub
                            dockerLoginAndPush(BACKEND_IMAGE_NAME)
                        }
                    }
                }
            }
        }
        stage('Deploy to OpenShift') {
            steps {
                script {
                    // Use OpenShift CLI or Jenkins Kubernetes plugin to deploy
                    sh "./sh"
                }
            }
        }
 
        
    }
 
    post {
        always {
            // Cleanup or additional steps after the pipeline
            script{
                echo "Always block executed!"
            }
        }
    
    }

}

def dockerLoginAndPush(imageName) {
        // Docker login to Docker Hub
        withCredentials([usernamePassword(credentialsId: DOCKER_HUB_CREDENTIALS, usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
            sh "docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD}"
            sh "docker push ${imageName}"
        }
}

```

## RUN Build pipeline


`Maintain following tree in git repository:`
```bash
frontend
    ├── Dockerfile
    └── ui
backend
    ├── Dockerfile
    └── jttours-0.0.1-SNAPSHOT.jar
kubernetes
    ├── backend
    │   ├── backend-configmap.yaml
    │   ├── backend-deployment.yaml
    │   └── backend-service.yaml
    ├── frontend
    │   ├── frontend-configmap.yaml
    │   ├── frontend-deployment.yaml
    │   └── frontend-service.yaml
    ├── mysql
    │   ├── mysql-configmap.yaml
    │   ├── mysql-deployment.yaml
    │   ├── mysql-pv.yaml
    │   ├── mysql-secret.yaml
    │   ├── mysql-service.yaml
    │   └── mysql-statefulset.yaml
    └── namespace.yaml
```
`frontend/Dockerfile`
```Dockerfile
FROM ubuntu:latest
MAINTAINER rahul_vishwakarma1
RUN apt-get update
RUN apt-get -y install curl gnupg
RUN curl -sL https://deb.nodesource.com/setup_14.x  | bash -
RUN apt-get -y install nodejs

COPY ./ui /home/ui

WORKDIR /home/ui

RUN useradd ui

RUN chmod -R ugoa+rwx /home/ui && chown -R ui:0 /home/ui

USER ui

EXPOSE 3000

RUN npm install
RUN mkdir -p node_modules/.cache && chmod -R 777 node_modules/.cache

CMD npm run build && npx serve -s build
#CMD ["npm", "start"]
```
`backend/Dockerfile`
```Dockerfile
FROM openjdk:17-jdk-alpine
MAINTAINER rahul_vishwakarma1
COPY . .
ENTRYPOINT ["java","-jar","/jttours-0.0.1-SNAPSHOT.jar"]
```
`sh`
```bash
#!/bin/bash
oc create ns jttours

# For MySQL Database
oc apply -f kubernetes/mysql/mysql-pv.yaml -n jttours
oc apply -f kubernetes/mysql/mysql-secret.yaml -n jttours
oc apply -f kubernetes/mysql/mysql-configmap.yaml -n jttours
oc apply -f kubernetes/mysql/mysql-statefulset.yaml -n jttours
oc apply -f kubernetes/mysql/mysql-service.yaml -n jttours

# For Backend
oc create configmap backend-configmap \
  --from-literal=SPRING_DATASOURCE_URL="jdbc:mysql://$(oc get svc mysql-service -n jttours -o jsonpath='{.spec.clusterIP}')/jttoursdb" \
  --from-literal=SPRING_DATASOURCE_USERNAME="root" \
  --from-literal=SPRING_DATASOURCE_PASSWORD="admin" \
  -n jttours

oc apply -f kubernetes/backend/backend-deployment.yaml -n jttours
oc apply -f kubernetes/backend/backend-service.yaml -n jttours
oc expose svc backend-service -n jttours


# For frontend
oc create configmap frontend-configmap \
  --from-literal=REACT_APP_API_URL=$(oc get route backend-service -n jttours -o jsonpath='{.spec.host}')\
  -n jttours

oc apply -f kubernetes/frontend/frontend-deployment.yaml -n jttours
oc apply -f kubernetes/frontend/frontend-service.yaml -n jttours
oc expose svc frontend-service -n jttours

oc get all -n jttours

echo http://$(oc get route frontend-service -n jttours -o jsonpath='{.spec.host}')
```

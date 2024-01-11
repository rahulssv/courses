# Kubernetes Hands-on 
## React + SpringBoot + MySQL Application
### 1. Dockerize Each Component:
**`Frontend Dockerfile`**
```Dockerfile 
FROM ubuntu:latest
MAINTAINER rahul_vishwakarma1
RUN apt-get update
RUN apt-get -y install curl gnupg
RUN curl -sL https://deb.nodesource.com/setup_14.x  | bash -
RUN apt-get -y install nodejs

# Copy only the necessary files and directories
COPY ./ui /home/ui
# Switch to the UI directory
WORKDIR /home/ui
# Create a non-root user and group, set proper permissions for the working directory
RUN useradd ui

RUN chmod -R ugoa+rwx /home/ui && chown -R ui:0 /home/ui
# Use a separate user for running the application
USER ui

# Expose the application port
EXPOSE 3000

# Install npm dependencies
RUN npm install
RUN mkdir -p node_modules/.cache && chmod -R 777 node_modules/.cache
# Specify the default command to run the application
CMD ["npm", "start"]
```
```bash
docker build -t rahul1181/frontend-image:1.16 . 
docker push rahul1181/frontend-image:1.16
```
> make sure to create .env file in ui containing url of pointing backend

**`Backend Dockerfile`**
```Dockerfile
FROM openjdk:17-jdk-alpine
MAINTAINER rahul_vishwakarma1
COPY . .
ENTRYPOINT ["java","-jar","/jttours-0.0.1-SNAPSHOT.jar"]
```
```bash
docker build -t rahul1181/backend-image:1.3 .
docker push rahul1181/backend-image:1.3 
```
### 2. Create Kubernetes Namespace:

 
**`namespace.yaml`**
```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: jttours
```
```bash
oc apply -f namespace.yaml
```
### 3. MySQL 
#### Persistent Storage:

 
**`mysql-pv.yaml`**
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: mysql-pv
  namespace: jttours
spec:
  capacity:
    storage: 250Mi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: "/path/to/mysql/data"
 
---
 
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mysql-pv-claim
  namespace: jttours
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 250Mi
```
```bash
oc apply -f mysql-pv.yaml
```
#### Create MySQL Secret:

 
**`mysql-secret.yaml`**
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: mysql-secret
  namespace: jttours
type: Opaque
data:
  mysql-root-password: YWRtaW4=   # Base64 encoded 'admin'
  mysql-user-password: YWRtaW4=   # Base64 encoded 'admin' 
```
```bash
oc apply -f mysql-secret.yaml
```
#### Create MySQL Configmap
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: mysql-config-map
  namespace: jttours
data:
  mysql-server: mysql-service    # The name of mysql service
  mysql-database-name: jttoursdb     # The name of the database used by the demo app
  mysql-user-username: rahul     # A new created user for the demo app 
  
```
```bash
oc apply -f mysql-configmap.yaml
```
#### MySQL StatefulSet
**`mysql-statefulset.yaml`**
```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: mysql-statefulset
  namespace: jttours
spec:
  serviceName: mysql-service
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      containers:
      - image: mysql:5.6
        name: mysql
        env:
        - name: MYSQL_DATABASE
          valueFrom:
            configMapKeyRef:
              name: mysql-config-map
              key: mysql-database-name
        - name: MYSQL_ROOT_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-secret
              key: mysql-root-password
        - name: MYSQL_USER
          valueFrom:
            configMapKeyRef:
              name: mysql-config-map
              key: mysql-user-username
        - name: MYSQL_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-secret
              key: mysql-user-password
        livenessProbe:
          tcpSocket:
            port: 3306
        ports:
        - containerPort: 3306
          name: mysql
        volumeMounts:
        - name: mysql-persistent-storage
          mountPath: /var/lib/mysql
      volumes:
      - name: mysql-persistent-storage
        persistentVolumeClaim:
          claimName: mysql-pv-claim
```
```bash
oc apply -f mysql-statefulset.yaml
```
#### MySQL Deployment (If MySQL StatefulSet is not applied )

> For databases statefulsets are preferred over deployments. It has its own advantages

**`mysql-deployment.yaml`**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql-deployment
  namespace: jttours
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
        tier: mysql
    spec:
      containers:
      - image: mysql:5.6
        name: mysql
        env:
        - name: MYSQL_DATABASE
          valueFrom:
            configMapKeyRef:
              name: mysql-config-map
              key: mysql-database-name
        - name: MYSQL_ROOT_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-secret
              key: mysql-root-password
        - name: MYSQL_USER
          valueFrom:
            configMapKeyRef:
              name: mysql-config-map
              key: mysql-user-username
        - name: MYSQL_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-secret
              key: mysql-user-password
        livenessProbe:
          tcpSocket:
            port: 3306
        ports:
        - containerPort: 3306
          name: mysql
        volumeMounts:
        - name: mysql-persistent-storage
          mountPath: /var/lib/mysql
      volumes:
      - name: mysql-persistent-storage
        persistentVolumeClaim:
          claimName: mysql-pv-claim

```
```bash
oc apply -f mysql-deployment.yaml
```
#### MySQL Service
```yaml
apiVersion: v1
kind: Service
metadata:
  name: mysql-service
  namespace: jttours
spec:
  selector:
    app: mysql
  ports:
    - protocol: TCP
      port: 3306
      targetPort: 3306
```
```bash
oc apply -f mysql-service.yaml
```

> paste the cluster-ip of mysql-service in backend-configmap.yaml

```bash
oc apply -f namespace.yaml
oc apply -f mysql-pv.yaml
oc apply -f mysql-secret.yaml
oc apply -f mysql-configmap.yaml
oc apply -f mysql-statefulset.yaml
# oc apply -f mysql-deployment.yaml
oc apply -f mysql-service.yaml
```
> paste cluster-ip of mysql-service in backend-configmap.yaml
### 4. Backend
#### Backend Configmap
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: backend-configmap
  namespace: jttours
data:
  SPRING_DATASOURCE_URL: "jdbc:mysql://172.21.171.36/jttoursdb" # cluster-ip of mysql-service
  SPRING_DATASOURCE_USERNAME: "root"
  SPRING_DATASOURCE_PASSWORD: "admin"
```
```bash
oc apply -f backend-configmap.yaml
```
#### Backend Deployment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: backend-deployment
  namespace: jttours
spec:
  replicas: 1
  selector:
    matchLabels:
      app: backend
  template:
    metadata:
      labels:
        app: backend
    spec:
      containers:
        - name: backend-container
          image: rahul1181/backend-image:1.2
          envFrom:
            - configMapRef:
                name: backend-configmap
          ports:
            - containerPort: 8080
          volumeMounts:
            - name: mysql-persistent-storage
              mountPath: /var/lib/mysql
      volumes:
        - name: mysql-persistent-storage
          persistentVolumeClaim:
            claimName: mysql-pv-claim
```
```bash
oc apply -f backend-deployment.yaml
```
#### Backend Service
```yaml
apiVersion: v1
kind: Service
metadata:
  name: backend-service
  namespace: jttours
spec:
  selector:
    app: backend
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
  type: NodePort
```
```bash
oc apply -f backend-service.yaml
```
```bash
oc expose svc backend-service -n jttours
```

> paste url of route in frontend-config

### 5. Frontend
#### Frontend Configmap
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: frontend-configmap
  namespace: jttours
data:
  REACT_APP_API_URL: "backend-service-jttours.ibm01-roks-2add6c5939e72723a23a68c764c76a06-0000.us-south.containers.appdomain.cloud"
```
```bash
oc apply -f frontend-configmap.yaml
```
#### Frontend Deploment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: frontend-deployment
  namespace: jttours
spec:
  replicas: 1
  selector:
    matchLabels:
      app: frontend
  template:
    metadata:
      labels:
        app: frontend
    spec:
      containers:
        - name: frontend-container
          image: rahul1181/frontend-image:1.15
          envFrom:
            - configMapRef:
                name: frontend-configmap
          ports:
            - containerPort: 3000
```
```bash
oc apply -f frontend-deployment.yaml
```
#### Frontend Service
```yaml
apiVersion: v1
kind: Service
metadata:
  name: frontend-service
  namespace: jttours
spec:
  selector:
    app: frontend
  ports:
    - protocol: TCP
      port: 80
      targetPort: 3000
  type: NodePort
```
```bash
oc apply -f frontend-service.yaml
```
```bash
oc expose svc frontend-service -n jttours
```
> Now we can access the frontend from route url
### 6. Ingress (Optional)
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-ingress
  namespace: jttours
spec:
  rules:
    - host: dns.rahulssv.com # Replace with your actual domain or IP address - Domain must be registered with service IP
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: frontend-service
                port:
                  number: 80
          - path: /api
            pathType: Prefix
            backend:
              service:
                name: backend-service
                port:
                  number: 80
```
```bash
oc apply -f ingress.yaml
```

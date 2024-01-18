# Sonarqube

- Sonarqube image comes with a temporary h2 database engine which is not recommended for production and doesn't persist across container restarts.
- We need to setup a database of our own and point it to Sonarqube at the time of starting the container.
- Sonarqube docker images exposes two volumes `"$SONARQUBE_HOME/data"`, `"$SONARQUBE_HOME/extensions"` as seen from Sonarqube Dockerfile.
- Since we wanted to persist the data across invocations, we need to make sure that a production grade database is setup and is linked to Sonarqube and the extensions directory is created and mounted as volume on the host machine so that all the downloaded plugins are available across container invocations and can be used by multiple containers (if required).

- Database Setup:

```bash
create database sonar;
grant all on sonar.* to `sonar`@`%` identified by "SOME_PASSWORD";
flush privileges;
```

- since we do not know the containers IP before hand, we use '%' for sonarqube host IP.
It is not necessary to create tables, Sonarqube creates them if it doesn't find them.

- Starting up Sonarqube container:

- create a directory on host
```bash
mkdir /server_data/sonarqube/extensions
mkdir /server_data/sonarqube/data # this will be useful in saving startup time
```

- Start the container
```bash
docker run -d \
    --name sonarqube \
    -p 9000:9000 \
    -e SONARQUBE_JDBC_USERNAME=sonar \
    -e SONARQUBE_JDBC_PASSWORD=SOME_PASSWORD \
    -e SONARQUBE_JDBC_URL="jdbc:mysql://HOST_IP_OF_DB_SERVER:PORT/sonar?useUnicode=true&characterEncoding=utf8&rewriteBatchedStatements=true&useConfigs=maxPerformance" \
    -v /server_data/sonarqube/data:/opt/sonarqube/data \
    -v /server_data/sonarqube/extensions:/opt/sonarqube/extensions \
    sonarqube
```

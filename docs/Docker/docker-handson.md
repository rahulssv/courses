# **`Docker hands-on demo:`**

Create a Docker Container:
1. Choose an application (e.g., a simple web server).
2. Write a Dockerfile to define the container.
3. Build the Docker image.
4. Run the container.
## `Server`
### `Dockerfile`
```Dockerfile
FROM ubuntu
RUN apt-get update
RUN apt-get -y install redis
EXPOSE 6379
CMD ["redis-server", "--protected-mode", "no"]
```
### `networkdetails`
```sh
[
    {
        "Name": "my-net",
        "Id": "8dcbda9dddb0245c0aec1e0427415550ce2794a06eebb29efeae2e6e99e32754",
        "Created": "2022-09-16T17:27:41.319816937Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.18.0.0/16",
                    "Gateway": "172.18.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {},
        "Options": {},
        "Labels": {}
    }
]
```
### `run`
```sh
docker network create "my-net" ;
docker network inspect my-net > networkdetails ;
echo created network ;
docker build -t server . ;
docker run -d --network my-net --network-alias red-server server ;

#add the optional -p 8080:6379 if you want to expose the redis port to host (in run command)
```

```sh
# Run follwind commands in terminal
cd Server
./run
```
## Client
### `Dockerfile`
```Dockerfile
FROM alpine:3.10

RUN apk add --update nodejs npm

RUN addgroup -S node && adduser -S node -G node

USER node

RUN mkdir /home/node/code

WORKDIR /home/node/code

EXPOSE 8080

COPY --chown=node:node package-lock.json package.json ./

RUN npm ci

COPY --chown=node:node . .

CMD ["node", "index.js"]
```
### `index.js`
```js
const express = require('express')
const app = express();
const axios = require('axios');
const Redis = require('redis');
const { json } = require('express');

const port = 8080

// const fetchApiData= async()=>{
//     const data=await axios.get('https://api.covidtracking.com/v1/states/current.json')
//     console.log("api req sned")
//     return dat
// }
const redisClinet = Redis.createClient(
  {
    host: process.env.REDIS_HOST,
    port: "6379",
  }
)


app.get('/', async (req, res) => {

  redisClinet.get('coronadata', async (err, cdata) => {
    if (err) console.error();
    if (cdata != null) {
      console.log("cache-hit")
      return res.json(JSON.parse(cdata))
    }
    else {
      console.log('cache-miss')
      const { data } = await axios.get("https://api.covidtracking.com/v1/states/current.json")
      redisClinet.setex('coronadata', 3600, JSON.stringify(data))
      res.json(data)
    }

  })

})

app.listen(port, () => {
  console.log(`App listening on port ${port}`);
})



// This function lets u exit the container by exiting node when u press Ctrl+C
process.on('SIGINT', function () {
  console.log("\nGracefully shutting down from SIGINT (Ctrl-C)");
  // some other closing procedures go here
  process.exit(0);
});

```

### `package.json`
```json
{
  "name": "corona_cache",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "axios": "^0.27.2",
    "express": "^4.18.1",
    "redis": "^3.0.0"
  }
}
```
### `run`
```sh
docker build -t client . ;
echo Image built. Now Running....
docker run -it -p 5000:8080  --network my-net -e REDIS_HOST=red-server client
```
```sh
# Run follwind commands in terminal
cd Client
./run
```
- Now click on port URL.

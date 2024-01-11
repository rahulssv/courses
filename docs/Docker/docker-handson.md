# **`Docker hands-on task:`**

Create a Docker Container:
1. Choose an application (e.g., a simple web server).
2. Write a Dockerfile to define the container.
3. Build the Docker image.
4. Run the container.


```
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

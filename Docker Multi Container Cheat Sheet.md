# Docker Multi Container Cheat Sheet

### Docker Network

<aside>
💡

docker network create ts-docker-net

</aside>

### No Image Build Needed For Mongo. Just Pull it From DockerHub

### Mongo DB Container

<aside>
💡

> docker run --name mongodb --rm -v ts-docker-db:/data/db --network ts-docker-net -e MONGO_INITDB_ROOT_USERNAME=ts-docker -e MONGO_INITDB_ROOT_PASSWORD=ts-docker mongo
> 
</aside>

### No Dockerfile Needed

### Node Express/Backend Image

<aside>
💡

docker build -t ts-docker-bakcend:v5 .

</aside>

### Node-Express/Backend Container

<aside>
💡

> docker run --name ts-docker-backend-container --rm --network ts-docker-net --env-file .env -w //app -v ts-docker-logs://app/logs -v "//$(pwd)"://app -v //app/node_modules -p 5000:5000 ts-docker-backend:v5
> 
</aside>

[Dockerfile [Nodejs]](https://www.notion.so/Dockerfile-Nodejs-2c1944bc44cc813dab3cd52396358bd7?pvs=21)

### NextJS/React/Frontend Image

<aside>
💡

docker build -t ts-docker-frontend:v5 .

</aside>

### NextJS/React/Frontend Container

<aside>
💡

> docker run --name ts-docker-frontend-conatiner --rm -p 3000:3000 --env-file .env.local -w //app -v "//$(pwd)"://app -v //app/node_modules --network ts-docker-net -e WATCHPACK_POLLING=true ts-docker-frontend:v5
> 
</aside>

[Dockerfile [NextJS/React/Frontend]](https://www.notion.so/Dockerfile-NextJS-React-Frontend-2c1944bc44cc81789b20d7c093fc89b3?pvs=21)

### Dockerfile [NextJS/React/Frontend]

FROM node:20

WORKDIR /app

COPY package.json .

RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "run", "dev"]

### .dockerignore

node_modules
dist
.vscode
.vercel
.env
.env.local
.env.development.local
.env.test.local
.env.production.local
.git


### See https://help.github.com/articles/ignoring-files/ for more about ignoring files.

### dependencies
/node_modules
/.pnp
.pnp.js
.yarn/install-state.gz
.vscode

### testing
/coverage

### next.js
/.next/
/out/

### production
/build

### misc
.DS_Store
*.pem

### debug
npm-debug.log*
yarn-debug.log*
yarn-error.log*

### local env files
.env*.local

### vercel
.vercel

### typescript
*.tsbuildinfo
next-env.d.ts

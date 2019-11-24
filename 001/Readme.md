## Use case angular container

Credits to:  [ https://dev.to/avatsaev/create-efficient-angular-docker-images-with-multi-stage-builds-1f3n](https://dev.to/avatsaev/create-efficient-angular-docker-images-with-multi-stage-builds-1f3n)



### Initialize an empty Angular project
```
ng new myapp
```
I will use insted the Docker contained ng 
```
docker run -u $(id -u) --rm -v "$PWD":/app trion/ng-cli ng new MyDemo
```

### nginx config
At the root of your Angular project, create nginx folder and create a file named default.conf with the following contents (./nginx/default.conf):
```
server {

  listen 80;

  sendfile on;

  default_type application/octet-stream;


  gzip on;
  gzip_http_version 1.1;
  gzip_disable      "MSIE [1-6]\.";
  gzip_min_length   1100;
  gzip_vary         on;
  gzip_proxied      expired no-cache no-store private auth;
  gzip_types        text/plain text/css application/json application/javascript application/x-javascript text/xml application/xml application/xml+rss text/javascript;
  gzip_comp_level   9;


  root /usr/share/nginx/html;


  location / {
    try_files $uri $uri/ /index.html =404;
  }

}
```

### Create the Docker file
```
### STAGE 1: Build ###

# We label our stage as ‘builder’
FROM node:10-alpine as builder

COPY package.json package-lock.json ./

## Storing node modules on a separate layer will prevent unnecessary npm installs at each build

RUN npm ci && mkdir /ng-app && mv ./node_modules ./ng-app

WORKDIR /ng-app

COPY . .

## Build the angular app in production mode and store the artifacts in dist folder

RUN npm run ng build -- --prod --output-path=dist


### STAGE 2: Setup ###

FROM nginx:1.14.1-alpine

## Copy our default nginx config
COPY nginx/default.conf /etc/nginx/conf.d/

## Remove default nginx website
RUN rm -rf /usr/share/nginx/html/*

## From ‘builder’ stage copy over the artifacts in dist folder to default nginx public folder
COPY --from=builder /ng-app/dist /usr/share/nginx/html

CMD ["nginx", "-g", "daemon off;"]
```

### I have both of the files ready I will just copy those
```
cp -r ../Dockerfile ../nginx ./
```


### Build the image command
```
docker build -t myapp .
```
### Run the container command
        
        the command will create a container using the IMAGE_NAME and run it
        the container will be present after it is stopped
        we can use the --rm switch to avoid prisisting the container
        - if we need a persistant container we better use --name switch to assign a decent name to the container
        - we can start the container afterwards using the "docker start [CONTAINER_NAME]" command which will start only an existing container using its name

```
docker run -p 8080:80 myapp
# will use this instead
docker run -p 8080:80 --rm  myapp
```
    this command will map the port 80 of the container to port 8080 of the host (docker host) 

Go to [http://localhost:8080](http://localhost:8080)

## Summary
What happened is that we added the declared dependencies, and compiled the source. 
Then created and Nginx image and copied over the compiled angular app from the builder tagged image.

## A good question would be:
- What if the source is changed and we need to rebuild
    - what we need to do is run the [build command](#/Build-the-image-command) again
        - the build process in the docker is optimized, as docker works in bulding layers for each command, if the pachages.json changes then all the subsequent layers are changes, but if only the other source files are changed that the npm install ( RUN npm ci && mkdir /ng-app && mv ./node_modules ./ng-app ) command has a ready layer from the previous build, because it depends on the layer with packages.json and this layer never changed. 


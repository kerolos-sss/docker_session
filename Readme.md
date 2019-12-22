# Docker
## Disclaimer 
### This Read me is made for a presentation, it is not self consistent, or undestandable by its own and not made to be used as a reference. It needs someone to tell the tale. But proceed if you you wish.

## It is working on my machine 

" Docker	is	an	open platform for	developers	and	sysadmins	to	build, ship, and run	distributed	applications.	Consisting	of	Docker	Engine,	a portable,	lightweight	runVme	and	packaging	tool,	and	Docker	Hub,	a	cloud	service	for	sharing	applications	and	automating	workflows,	Docker	enables	apps	to	be	quickly	assembled	from	components	and	eliminates	the	friction	between	development,    QA,	and	producton environments. "	

* definition and images credit to Chris Tankersley https://www.slideshare.net/ctankersley/docker-for-developers-60673839?from_action=save

## Normal Bare-Metal Server 
![Normal Bare-Metal Server Diagram](static/images/normal_bare_metal_server.png)

## Virtual Machines
![Virtual Machines Diagram](static/images/virtual_machines.png)

## Containers
![Containers Diagram](static/images/containers.png)

## Getting Started



### Docker Registery

A Docker Registry is a repository for Docker Images

### Images

    A docker Image is a file system with some metadata, built by us or other party to containt an application with its dependencies. 

### Docker Container

- When running an image a container is created holding a Volume that represents the Image and the application can run in.

- When a container is started the the first command assigned in metadata is run inside it.

- Usually a container will run a single process as a service or as a utility.

### Volumes

- A Docker volume is a filesystem that can be mounted on a docker container.
- Usually a docker has one volume, but more than one volumes can be mounted on it.

- -v will mount a volume when running the container

### Networks

- A docker image will have network access through a bridge interface by default.
- other custom networks my be added to the container
- a container may be linked with other containers through network aliases 


## Docker commands

### docker run

#### will run	a container	

```
docker	run	[opVons]	IMAGE	[command]	[arguments]	
```

#### [opVons	]modify	the	docker	process	for	this	container	

#### IMAGE	is	the	image	to	use	

#### [command]	is	the	command	to	run	inside	the	container	

#### [arguments] are arguments for the	command	that is run inside the container


credits to [docker-curriculum](https://docker-curriculum.com/) 

```
$ docker run hello-world

Hello from Docker.
This message shows that your installation appears to be working correctly.
...
```

just pulling an image 

```
docker pull busybox
```

Just running
```
docker run busybox
```

Custome command
```
docker run busybox echo "hello from busybox"
```

Display running continers
```
docker ps
```

dispaly all containers
```
docker ps -a
```

Run and attach shell to a container
```
docker run -it busybox sh
```

Starting existing docker
```
docker start CONTAINER_NAME

docker start 305297d7a235
```


- each time we run an image a new container is created 
- how to avoid this
    - giving the container a name. --name
    - removing the container once finished --rm
```
docker start CONTAINER_NAME

```

--name
```
docker run --name myContiner hellow-world
```
Removing a container
```
docker rm myContainer ff0a5c3750b9
```

removing the container after running
```
docker run --rm hello-world
```

Website
```
docker run --rm prakhar1989/static-site
```
how to access our website

```
docker run -d -P --name static-site prakhar1989/static-site
```
-P will map all exposed port to arbitrary ports on our host



```
docker port
```

Will show us the ports exposed
```
docker run -p 8888:80 --name static-container prakhar1989/static-site
```
will mapp host ports ports to spesific ports in the container


## trouble shooting
```
docker ps
docker ps -a
```
tapping into a working docker  
this means running another command along side the deomon running on the port

```
docker exec --it CONTAINER_NAME
```

```
docker exec --it static-container
```










## Using docker to ececute simgle comaand


- Angular cli in a docker
    ```
    docker run -u $(id -u) --rm -v "$PWD":/app trion/ng-cli ng new MyDemo
    cd MyDemo
    docker run -u $(id -u) --rm -v "$PWD":/app trion/ng-cli ng build
    ```

## Next

[000 Docker file](000/Readme.md)

[001 Dockerfile](001/Readme.md) 

[002 docker-compose](002/Readme.md)




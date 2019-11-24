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

### docker run

#### will	run	a	container	

#### This	will	not	restart	an	exisVng	container,	just	create	a	new	one

```
docker	run	[opVons]	IMAGE	[command]	[arguments]	
```

#### [opVons	]modify	the	docker	process	for	this	container	

#### IMAGE	is	the	image	to	use	

#### [command]	is	the	command	to	run	inside	the	container	

#### [arguments] are arguments for the	command	that is run inside the container


- each time we run an image a new container is created 
- how to avoid this
    - giving the container a name.
    - removing the container once finished


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

## Using docker to ececute simgle comaand


- Angular cli in a docker
    ```
    docker run -u $(id -u) --rm -v "$PWD":/app trion/ng-cli ng new MyDemo
    cd MyDemo
    docker run -u $(id -u) --rm -v "$PWD":/app trion/ng-cli ng build
    ```

## Next

[001 Dockerfile](001/Readme.md) 

[002 docker-compose](002/Readme.md)




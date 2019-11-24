# Docker

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
• IMAGE	is	the	image	to	use	
• [command]	is	the	command	to	run	inside	the	container	
• [arguments]	are	arguments	for	the	command	
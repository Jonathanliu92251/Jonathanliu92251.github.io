# 1 Welcome to Docker
## 1.1 What's Docker ?
Container  - **concealed processes**  
Container are not virtualization  - **unix process**  
Running software in containers for isolation  - **inter-process interruption**  
Shipping containers - **image**  

![Docker](../img/dockinaction/01container.png)

## 1.2 What problems does Docker solve ?
1. Getting orgainzed  - **junk drawer to isolated container & images**
![old](../img/dockinaction/dockinaction/02mess.png)
![new](../img/dockinaction/03tidycontainer.png)

2. Improving portability  

- Using a virtual machine to contain a single program is wasteful. 
- This is especially so when you’re running several virtual machines on the same computer.
- Docker uses a single, small virtual machine to run all the containers. 
- By taking this approach, the overhead of running a virtual machine is fixed while the number of containers can scale up.
Portecting your computer

![new](../img/dockinaction/04isolation.png)
## 1.3 Why is Docker important ?
1. easier for sys adm & software dev (container abstraction & tooling)
2. push forward by large software companies & community
3. same apps store for all mobile devices ( install, compartmentalization & remove)
4. possible isolation of operation systems

## 1.4 Where & Wehn to use Docker ?
1. NOT for OS X or Windows native application
2. NOT for security programs that have to run with full access to the machine
2. software that typically runs on a Linux server or desktop
3. add in-depth defense
4. Keep compute clean 

![old](../img/dockinaction/05dockerrunA.png)
![new](../img/dockinaction/06dockerrunA.png)

# 2. Running software in containers
## 2.1 Get help with Docker command line
**docker help**

```
Management Commands:
  config      Manage Docker configs
  container   Manage containers
  image       Manage images
  network     Manage networks
  node        Manage Swarm nodes
  plugin      Manage plugins
  secret      Manage Docker secrets
  service     Manage services
  stack       Manage Docker stacks
  swarm       Manage Swarm
  system      Manage Docker
  volume      Manage volumes

Commands:
  attach      Attach local standard input, output, and error streams to a running container
  build       Build an image from a Dockerfile
  commit      Create a new image from a container's changes
  cp          Copy files/folders between a container and the local filesystem
  create      Create a new container
  diff        Inspect changes to files or directories on a container's filesystem
  events      Get real time events from the server
  exec        Run a command in a running container
  export      Export a container's filesystem as a tar archive
  history     Show the history of an image
  images      List images
  import      Import the contents from a tarball to create a filesystem image
  info        Display system-wide information
  inspect     Return low-level information on Docker objects
  kill        Kill one or more running containers
  load        Load an image from a tar archive or STDIN
  login       Log in to a Docker registry
  logout      Log out from a Docker registry
  logs        Fetch the logs of a container
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  ps          List containers
  pull        Pull an image or a repository from a registry
  push        Push an image or a repository to a registry
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  rmi         Remove one or more images
  run         Run a command in a new container
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  search      Search the Docker Hub for images
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  version     Show the Docker version information
  wait        Block until one or more containers stop, then print their exit codes
```
## 2.2 Controlling container: build a website monitor
```
docker logs 
docker run / start /stop / restart /pause
docker kill / rm
docker ps / inspect / exec
docker images / rmi
docker search / pull /save /tag
```
![2.1 Example](21Example.png)
## 2.3 Solved problems and the PID namespace
Here are some common conflict problems:   

- Two programs want to bind to the same *network port*.
- Two programs use the same *temporary filename*, and file locks are preventing
that.
- Two programs want to use different versions of some globally installed *library*.
- Two copies of the same program want to use the *same PID file*.
- A second program you installed *modified an environment variable* that another
program uses. Now the first program breaks.

Docker solves software conflicts with such tools as *Linux namespaces, file system roots, and virtualized network components*. All these tools are used to provide isolation to each container.

![2.2 solve](../img/dockinaction/22Problem.png)
## 2.4 Eliminating metaconflicts: building a website farm
1. Container ID, abbreviated container ID, or its human-friendly name.  
	**PID:** hex-encoded 1024-bit numbers, or 16 * heximal characters:  
	7cb5 d2b9 a7ea b87f 0718 2b5b f589 36c9 9478 9099 5b1b 94f4 1291 2fa8 22a9 ecb5  
	
	**CID file** uses known names in a global (Docker-wide) namespace: `docker create --cidfile /tmp/web.cid nginx`.  Docker won’t create a new container using the provided CID file if that file already exists. The command will fail just as it does when you create two containers with the same name.  
2. All containers are in any one of four distinct states: running, paused, restarting, or exited.

  ![2.3 Container Status](../img/dockinaction/23ContainerStat.png)

## 2.5 Building enviornment-agnostic systems
1. Read-only file systems  
	Using the --read-only flag at container-creation time will mount the container file system as read-only and prevent specialization of the container. 
	 
	docker run -d --name wp *--read-only* wordpress:4  

2. Environment variable injection  
docker create \   
    --env WORDPRESS_DB_HOST="my database hostname" \  
    --env WORDPRESS_DB_USER=site_admin \  
    --env WORDPRESS_DB_PASSWORD=MeowMix42 \  
      wordpress:4

## 2.6 Building duarable containers
1. Automatically restarting containers  
	Using the --restart flag at container-creation time, you can tell Docker to do any of the following:    
	■ Never restart (default)  
	■ Attempt to restart when a failure is detected  
	■ Attempt for some predetermined time to restart when a failure is detected  
	■ Always restart the container regardless of the condition  
	
	Docker uses an exponential backoff strategy for timing restart attempts.  
	LAMP stack (Linux, Apache, MySQL, PHP)

2. Keeping containers running with supervisor and startup processes  
	kill a process inside of a container from within that con- tainer, you need to know the PID in the container’s PID namespace. 
	
	`
	docker top lamp-test,     
	docker exec lamp-test ps
	` 
	
	A common alternative to the use of init or supervisor programs is using a startup script that at least checks the preconditions for successfully starting the contained soft- ware. These are sometimes used as the default command for the container. 

## 2.7 Cleaning up
1. remove / kill containers  
docker rm -vf $(docker ps -a -q)

2. remove images  
docker rmi  -f $(docker images)


#3.Software installation simplified
![StoryLine](../img/dockinaction/31storyline.png)
##3.1 Identify software
**image ID, repository, Tag**  
  A repository is a named bucket of images. The name is similar to a URL. A repository’s name is made up of the name of the host where the image is located, the user account that owns the image, and a short name.  
  ![repository](../img/dockinaction/32repository.png)

##3.2 Find & Install
  ![Dockerhub](../img/dockinaction/33dockerhub.png)
DockerHub: [https://hub.docker.com](https://hub.docker.com)  
docker login / logout  
docker search
docker run  
docker load / save
docker images / rmi  

4 ways to install software:

1. DockerHub repository by default:  
  `docker run -it dockerinaction/ch3_ex2_hunt`

2. use alternative repository registries or run your own registry. REGISTRYHOST/USERNAME/NAME:TAG
  `docker pull quay.io/dockerinaction/ch3_hello_registry:latest ` 

3. manually load images from a file.  
	
	`docker pull busybox:latest`  
	`docker save -o myfile.tar busybox:latest`   
	`docker rmi busybox`  
	`docker load –i myfile.tar`
	
4. download a project from some other source and build an image using a provided Dockerfile.
	`git clone https://github.com/dockerinaction/ch3_dockerfile.git` 
	`docker build -t dia_ch3/dockerfile:latest ch3_dockerfile`

##3.3 Container file system abstraction and isolation
![Layer relationships](../img/dockinaction/34layer.png)

1. union file system  
create mount points on your host’s file system that abstract the use of layers. The layers created are what are bundled into Docker image layers.  
when a Docker image is installed, its layers are unpacked and appro- priately configured for use by the specific file system provider chosen for your system.  

  PROS: single copy, seperation  
  CONS: compatible for different file systems.
2. MNT namespaces  
The Linux kernel provides a namespace for the MNT system. When Docker creates a container, that new container will have its own MNT namespace, and a new mount point will be created for the container to the image.
3. chroot system call.  
make the root of the image file system the root in the con- tainer’s context. This prevents anything running inside the container from referenc- ing any other part of the host file system.

#4. Persistent storage and shared state with volumes
##4.1 Introducing volumes
![container & storage](../img/dockinaction/41.png)

* A *volume* is a mount point on the con- tainer’s directory tree where a portion of the host directory tree has been mounted.
* images are appropriate for packaging and distributing relatively static files like programs; volumes hold dynamic data or specializations. 
* This distinction makes images reusable and data simple to share. 


volume container.  
![creating and recovering data persisted](../img/dockinaction/42.png)

1. Specify volume mount point inside the container:
	
		docker run -d \  
		    --volume /var/lib/cassandra/data \
		    --name cass-shared \
		    alpine echo Data Container
    
2. Inherit volume definitions

		docker run -d \
		    --volumes-from cass-shared \
		    --name cass1 \
		    cassandra:2.2
3. run a Cassandra client tool and connect to your running server
		    
		docker run –it --rm \
		    --link cass1:cass \
		    cassandra:2.2 cqlsh cass

##4.2 Volume type
**Bind mount volumes** use any user-specified directory or file on the host operating system

		docker run -d --name bmweb \
		    -v ~/example-docs:/usr/local/apache2/htdocs \
		    -p 80:80 \
		    httpd:latest
**Managed volumes** use locations of Docker managed space,  created by the Docker daemon in space controlled by the daemon

		docker run -d \
		    -v /var/lib/cassandra/data \
		    --name cass-shared \
		    alpine echo Data Containe
![Volume Type](../img/dockinaction/43.png)

##4.3 Sharing volumes
1. Host-dependent sharing  
created four containers, each of which mounted the same direc- tory as a volume. The first two containers are writing to different files in that volume. The third and fourth containers mount the volume at a different location and as read- only. 

		docker run --name woolf -d \
		            --volume ~/web-logs-example:/data \
		            dockerinaction/ch4_writer_a
		docker run --name alcott -d \
		            -v ~/web-logs-example:/data \
		            dockerinaction/ch4_writer_b
		docker run --rm --entrypoint head \
		            -v ~/web-logs-example:/towatch:ro \
		            alpine:latest \
		            /towatch/logA
		docker run --rm \
		            -v ~/web-logs-example:/toread:ro \
		            alpine:latest \
		            head /toread/logB
2. Generalized sharing
![Volume Sharing](../img/dockinaction/44.png)


* The docker run command provides a flag that will copy the volumes from one or more containers to the new container. 
* The flag --volumes-from can be set multiple times to specify multiple source containers.		

		#create 2 volume: fowler, knuth    
		docker run --name fowler \
		            -v ~/example-books:/library/PoEAA \
		            -v /library/DSL \
		            alpine:latest \
		            echo "Fowler collection created."
		            
		docker run --name knuth \
		    -v /library/TAoCP.vol1 \
		    -v /library/TAoCP.vol2 \
		    -v /library/TAoCP.vol3 \
		    -v /library/TAoCP.vol4.a \
		    alpine:latest \
		    echo "Knuth collection created"
		
		#List all volumes as they were copied into new container    
		docker run --name reader \
		    --volumes-from fowler \
		    --volumes-from knuth \
		    alpine:latest ls -l /library/
		    
		#Checkout volume list for reader    
		docker inspect --format "{{json .Volumes}}" reader    
 
* You can copy volumes directly or transitively. 
   
		#Create an aggregation
		docker run --name aggregator \
		    --volumes-from fowler \
		    --volumes-from knuth \
		    alpine:latest \
		    echo "Collection Created."
		
		#Consume volumes from a single source and list them                            
		docker run --rm \
		    --volumes-from aggregator \
		    alpine:latest \
		    ls -l /library/

##4.4 The managed volume life cycle
docker rm -v student

##4.5 Container patterns
1. volume container  
	* keeping a handle on data even in cases where a single container should have exclusive access to some data. These handles make it possible to easily back up, restore, and migrate data.
	* keeping your volumes organized and avoiding the orphan volume problem.

2. Data-packed volume container  
	* distribute static resources like configuration or code for use in containers created with other images.  
	* A data-packed volume container is built from an image that copies static content from its image to volumes it defines. In doing so, these containers can be used to dis- tribute critical architecture information like configuration, key material, and code. 
	* distributing static con- tent for other containers.

			Copy image content into a volume
			docker run --name dpvc \
			    -v /config \
			    dockerinaction/ch4_packed /bin/sh -c 'cp /packed/* /config/'
			
			List shared material
			docker run --rm --volumes-from dpvc \
			    alpine:latest ls /config    
			
			View shared material
			docker run --rm --volumes-from dpvc \
			    alpine:latest cat /config/packedData
			Remember to use –v when you clean up
			docker rm -v dpvc
3. Polymorphic container  
	* provides some functionality that’s easily substituted using volumes.   
	* compose minimal functional components and maximize reuse.		 

#5. Network exposure
##5.1 Concepts
![Basics: protocols, interfaces, and ports](../img/dockinaction/51.png)
![Bigger: networks, NAT, and port forwarding](../img/dockinaction/52.png)
##5.2 Docker Container Networking
![4 archetypes](../img/dockinaction/53.png)

###1. Closed containers

		#Create a closed container, list the interfaces
	    docker run --rm \
	    --net none \
	    alpine:latest \
	    ip addr
	    
	    #Test by ping Google -"“ping: send-to: Network is unreachable.” 
	    docker run --rm \
	    --net none \
	    alpine:latest \
	    ping -w 2 8.8.8.8 

  - doesn’t allow any network traffic, access to the network or the internet won’t operate correctly 
  - access only to a loopback interface, only communicate with themselves or each other
  - Use case: network isolation is the highest or whenever a program doesn’t require network access. eg. 
     - Running a terminal text editor
     - Running a program to generate a random password

###2. Bridged containers
have a private loopback interface and another private interface that’s connected to the rest of the host through a network bridge

		#Create a closed container, list the interfaces
	    docker run --rm \
	    --net bridge \
	    alpine:latest \
	    ip addr
	    
	    #Test by ping Google -"“ping: send-to: Network is unreachable.” 
	    docker run --rm \
	    --net bridge \
	    alpine:latest \
	    ping -w 2 8.8.8.8 


**2.1 reach out**
		
		docker run --rm \
    		--net bridge \
    		alpine:latest \
		    ip addr
		    
		docker run --rm \
    		--net bridge \
    		alpine:latest \
    		ping -w 2 8.8.8.8    
    		
**2.2 Custom name resolution (hostname)**

		#Set the container host name, resolve to an IP address
		docker run --rm \
	    	--hostname barker \
   		 	alpine:latest \
    		nslookup barker    		
    		
    	===>
			Name:      barker
			Address 1: 172.17.0.22 barker	
			
**2.2 Custom name resolution (DNS assignment)**

		#Set primary DNS server, Resolve IP address of docker.com
		docker run --rm \ 
			--dns 8.8.8.8 \ 
			alpine:latest \
    		nslookup docker.co
    			
**2.2 Custom name resolution (DNS Search order)**

    	#Set search domain, Look up shortcut for registry.hub.docker.com
    	docker run --rm \
    		--dns-search docker.com \
    		busybox:latest \
    		nslookup registry.hub
    	docker run --rm \
    		--dns-search docker.com  \
    		--dns-search myothercompany ...
**2.2 Custom name resolution (DNS override)**

		# add an entry on /etc/hosts
		docker run --rm \
			--hostname mycontainer \
    		-add-host docker.com:127.0.0.1 \
    		--add-host test:10.10.10.2 \
    		alpine:latest \
    			cat /etc/hosts
**2.3 Opening inbound communication**  
	If DNS is your best tool for changing outbound traffic behavior, then the firewall and network topology is your best tool for controlling inbound traffic.
	![An inbound traffic route to a bridged container](../img/dockinaction/54.png)  
	
	Example | Comment
	---------+----------
	docker run -p 3333 | host:* to container:3000
	docker run -p 3333:3333 | host:3000 to container:3000
	docker run -p 192.168.0.32::2222 | 192.168.0.32:* to container:2222
	docker run -p 192.168.0.32:1111:1111 | 192.168.0.32:1111 to container:1111
	
	- "--publish-all" or "-P", to expose all available
	- docker ps / inspect / port, see the mappings.

**2.4 Inter-container communication**

* Allowing communication in this way makes it simple to build cooperating contain- ers. No additional work needs to be done to build pipes between containers. It’s as free as an open network.
* you can configure it to disallow network con- nections between containers. by setting --icc=false 
* When inter-container communication is disabled, any traffic from one container to another will be blocked by the host’s firewall except where explicitly allowed.
	
![Inter-container communication](../img/dockinaction/55.png)
	
**2.5 Modifying the bridge interface**

* Define the address and subnet of the bridge. `docker -d --fixed-cidr "192.168.0.192/26`
* Define the range of IP addresses that can be assigned to containers
* Define the maximum transmission unit (MTU). `docker -d –mtu 1200`

###3. Joined containers
* These containers share a common network stack. 
* In this way there’s no isolation between joined containers. 
* This means reduced control and security.  
* The best reasons to use joined containers
	1. Use joined containers when you want to use a single loopback interface for commu- nication between programs in different containers.
	1. Use joined containers if a program in one container is going to change the joined net- work stack and another program is going to use that modified network.
	1. Use joined containers when you need to monitor the network traffic for a program in another container.
	
			docker run -d --name brady \
			    --net none alpine:latest \
			    nc -l 127.0.0.1:3333
			docker run -it \
			    --net container:brady \
			    alpine:latest netstat –al

###4. Open containers
have no network container and have full access to the host’s network.
provide absolutely no isolation  
processes can bind to protected network ports numbered lower than 1024.


	docker run --rm \
	    --net host \
	    alpine:latest ip addr

![open container](../img/dockinaction/511.png)

## Inter-container dependencies

### 3 approaches:
Bridge network. assigns IP addresses to containers dynamically at creation time, local service discovery can seem complicated.

1. use a local DNS server and a registration hook when containers start.
   * handle dynamic environments
2. write a programs to scan the local network for IP addresses listening on known ports.
	* require a non-trivial workload and additional tooling
	* fail if arbitrary inter-container communication has been disabled.
	* force all traffic out and back through the host’s interface to known published ports.
3. links for local service discovery

### links for local service discovery
When you create a new container, tell Docker to link it to any other running container.
Adding a link on a new container does three things:

* Environment variables describing the target container’s end point will be cre- ated.
* The link alias will be added to the DNS override list of the new container with the IP address of the target container.
* Most interestingly, if inter-container communication is disabled, Docker will add specific firewall rules to allow communication between linked containers.

		# Named target of a link
		docker run -d --name importantData \
		    --expose 3306 \
		    dockerinaction/mysql_noauth \
		    service mysql_noauth start
		    
		# Create link and set alias to db     
		docker run -d --name importantWebapp \
		    --link imporantData:db \
		    dockerinaction/ch5_web startapp.sh -db tcp://db:3306
		
		# This container has no route to importantData.
		docker run -d --name buggyProgram \
		    dockerinaction/ch5_buggy    
		    
#6. Limiting risk with isolation

Containers provide isolated process contexts, not whole system virtualization. The semantic difference may seem subtle, but the impact is drastic. What to cover:

* how to give containers resource allowances
* open access to shared memory
* run programs as specific users
* control the type of changes that a container can make to your computer
* integrate with otherLinux isolation tools.

![Eight-sided containers](../img/dockinaction/61.png)

##1. Resource Allowance

docker run / create [ memory | CPU | device ] [ n units ]

	# Set a memory constraint
	docker run -d --name ch6_mariadb \
	    --memory 256m \
	    --cpu-shares 1024
	    --user nobody \
	    --cap-drop all \
	    dockerfile/mariadb
	    
	# Set a relative process weight on CPU
	docker run -d -P --name ch6_wordpress \
		--memory 512m \
		--cpu-shares 512 \
		--user nobody \
		--cap-drop net_raw \
		--link ch6_mariadb \
		wordpress:4.1 

	# Restrict to CPU number 0
	docker run -d \
 		--cpuset-cpus 0 \
		--name ch6_stresser 
		dockerinaction/ch6_stresser	
	
	# Mount video0	
	docker -it --rm \
    	--device /dev/video0:/dev/video0 \
    	ubuntu:latest ls -al /dev
##2. Shared memory
###(1)Sharing IPC primitives between containers: "--IPC"
	#Start producer
	docker -d -u nobody
		--name ch6_ipc_producer \
	   dockerinaction/ch6_ipc -producer
	
	#Start consumer
	docker -d 
		 --name ch6_ipc_consumer \
	    --ipc container:ch6_ipc_producer \
	    dockerinaction/ch6_ipc -consumer 
	
	#view data produced & consumed
	docker logs ch6_ipc_producer
	docker logs ch6_ipc_consumer
	
	#remove
	docker rm -vf ch6_ipc_producer ch6_ipc_consumer

![Shared memeroy](../img/dockinaction/62.png)

###(2)Using an open memory container

	# Start a producer, Use open memory container
	docker -d --name ch6_ipc_producer \
	    --ipc host \
	    dockerinaction/ch6_ipc –producer
	
	# Start a consumer, Use open memory container
	docker -d --name ch6_ipc_consumer \
	    --ipc host \
	    dockerinaction/ch6_ipc -consumer
	    
	# Clean up
	docker rm -vf ch6_ipc_producer ch6_ipc_consumer

##3. Users
**USR namespace**. File system inside a container,  except for volume, will not be impactedby inherited user privilege. 

* Displays the metadata of a specific container: `docker inspect [ container ]`
* the run-as user might be changed by whatever script the image uses to start up: boot, or init, scripts. Thus as this ` docker run --rm --entrypoint "" busybox:latest whoami` or `id`
* Get a list of available users in an image. `docker run --rm busybox:latest awk -F: '$0=$1' /etc/passwd`
* you might consider learning to start setting passwords or disabling the root account like Ubuntu and others. 
* The best way to be confident in your runtime configuration is to pull images from trusted sources or build your own.

		# Set run-as user:group
		docker run --rm \
		    -u 10000:20000 \
		    busybox:latest id
##4. run w/ Privileged user: --privileged
docker create or docker run 

docker run --rm 
    --privileged 
    ubuntu:latest id

also fully network

docker run --rm 
    --privileged 
    --host 
    ubuntu:latest id
##5. Build use-case-appropriate containers

In reality, people tend to be a bit more reactive than proactive.Start with the most isolated container you can build and justify reasons for weakening those restrictions. 

The best approach is to isolate the risk. 

1. Make sure the application is running as a user with limited permissions. That way, if there’s a problem, it won’t be able to change the files on your computer.
2. Limit the system capabilities of the browser. In doing so, you make sure your system configuration is safer. 
3. Set lim-its on how much of the CPU and memory the application can use. Limits help reserve resources to keep the system responsive. 
4. Specifically whitelist devices that it can access. That will keep snoops off your webcam, USB, and the like.
    
	
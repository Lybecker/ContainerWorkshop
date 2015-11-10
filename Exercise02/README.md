#Docker CLI

Now that we have a virtual machine running with Docker on Azure we can test it out by running a Container.

1. Open SSH tunnel to your Docker host 

>You'll need a SSH client like [putty](http://www.putty.org/).

2. Type the following command in the terminal: 

	```
	$ docker run hello-world
	```
	If Docker is configured correctly you should see an output like so.
	
	```
	Unable to find image 'hello-world:latest' locally
	latest: Pulling from library/hello-world
	b901d36b6f2f: Pull complete
	0a6ba66e537a: Pull complete
	Digest: sha256:517f03be3f8169d84711c9ffb2b3235a4d27c1eb4ad147f6248c8040adb93113
	Status: Downloaded newer image for hello-world:latest
	
	Hello from Docker.
	This message shows that your installation appears to be working correctly.
	
	To generate this message, Docker took the following steps:
	1. The Docker client contacted the Docker daemon.
	2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
	3. The Docker daemon created a new container from that image which runs the
		executable that produces the output you are currently reading.
	4. The Docker daemon streamed that output to the Docker client, which sent it
		to your terminal.
	
	To try something more ambitious, you can run an Ubuntu container with:
	$ docker run -it ubuntu bash
	
	Share images, automate workflows, and more with a free Docker Hub account:
	https://hub.docker.com
	
	For more examples and ideas, visit:
	https://docs.docker.com/userguide/
	```
	
	First the hello-world image is downloaded to the Docker host. It is the same as doing a pull operation.
	It automatically retrieves the latest version, if not specified.
	Then the container is started and outputs the above content.
	
3. Now try to download an Ubuntu images

	```
	$ docker pull ubuntu
	```
	It will download the latest Ubunto image from Docker Hub.

4. List the images on the Docker host

	```
	$ docker images
	```
5. Start a Ubuntu container
	```
	$ docker run -i -t ubunto /bin/bash
	```
	The  -i  flag starts an interactive container meaning that the prompt we enter will be from within the container. The  -t  flag creates a pseudo-TTY that attaches  stdin  and  stdout .
	
	To detach the TTY without exiting the shell, use the escape sequence  Ctrl-p  +  Ctrl-q . The container will continue to exist in a stopped state once exited. To list all containers, stopped and running use the  docker ps -a  command.

6. List running containers
	```	
	$ docker ps
	
	#Lists all containers
	$ docker ps -a
	```
7. Let's create a long running container and assign it a name
	```
	# Start a long running process
	$ docker run -d -name=my-ubuntu ubuntu /bin/sh -c "while true; do echo Hello world; sleep 1; done"
	
	# Collect the output of the job so far
	$ docker logs my-ubuntu
	
	# Kill the job
	$ docker kill my-ubuntu
	```	
8. Inspecting our container
	Lastly, we can take a low-level dive into our Docker container using the docker inspect command. It returns a JSON hash of useful configuration and status information about Docker containers.
	```
	$ docker inspect container_name
	```
#Updating an image

There are two ways of updating an image. We can either create a 
Dockerfile with the instructions needed to create the desired 
image, or we can commit our changes to an image. 
Since we'll be diving into Dockerfiles in the next section we'll 
look at commiting changes to an image here.

To update an image we first need to create a container from the 
image we'd like to update.

```
$ docker run -t -i microsoft/aspnet /bin/bash
root@0b2616b0e5a8:/#
```

>**Note:** Take note of the container ID that has been created, `0b2616b0e5a8`, as we'll need it in a moment (this is the short id of the container).

Inside our running container we can add a few files (via the rouch command) or install something using `apt-get`. 
For simplicity we'll just create a few files, and once that is done we'll exit our container using the `exit` command.

Now that we have an image with the few changes that we made. 
We can then commit a copy of this container to an image using 
the `docker commit` command.

```
$ docker commit -m "Added my files" -a "Anders Lybecker" \
0b2616b0e5a8 ouruser/aspnet:v2
4f177bd27a9ff0f6dc2a830403925b5360bfe0b93d476f7fc3231110e7f71b1c
```

Here we've used the docker commit command. We've specified two flags: 
`-m` flag which allows us to specify a commit message, 
and the `-a` flag which allows us to specify an author for our update.

We've also specified the container we want to create this new image from, 
`0b2616b0e5a8` (the Id we noted earlier) and we've specified a target for the image as well:

```
myuser/aspnet:v2
```

Now, lets list our images again using the `docker images` command. 
The list should now contain the image that was pulled and our updated version under "myuser".

You can run this image with the following command and verify that the added files are in fact there.

```
$ docker run -t -i myuser/aspnet:v2 /bin/bash
```

##Remove an image from the host

You can remove any images from your host as desired using the `docker rmi` command.

In the following example we'll remove the `aspnet` image we created before.

```
$ docker rmi myuser/aspnet
```
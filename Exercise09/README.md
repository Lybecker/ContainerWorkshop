#Dockerhub

Docker hub is a hosted repository for all your docker images.
It's possible to both use public and private repos, just like github!

1. First we need to go to http://hub.docker.com and create a user.
2. Then we need to login inside our docker host with that user.
```
docker login
```
3. When you are logged in, it's now possible to get access to your repository.
```
docker push <username>/<repo>:[tag]
```
4. Before we can actually push the image we have to build it in a special way, we need to name it ```<username>/<repo>:[tag]```, so we need to rebuild our image to be pushed to Docker Hub.
5. So just like we did previously, we run docker build, this time just with another name of the image.
```docker build -t  <username>/<repo>:[tag] .```
6. And now we can push it to the Docker Hub.
7. ```docker push <username>/<repo>:[tag]```

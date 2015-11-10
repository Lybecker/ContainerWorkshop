#Deploying containers with Dockerfile
Docker files are the second way of deploying containers.
Instead of manually configuring the server and commiting the changes, we can do it all from a script.

1. Open Visual Studio Code and create a new Dockerfile. (Open VS Code and save the file as a Dockerfile, no extension)
2. Add the following lines to the file
```
FROM nginx
RUN apt-get update && apt-get install -y wget
WORKDIR /usr/share/nginx/html/
RUN rm index.html
RUN wget https://raw.githubusercontent.com/JesperJakobsen/Dockerdemo/master/index.html
```
3. Copy the text
4. Create a new folder the host with ```mkdir <folder>```, then change your working directory to that folder ```cd foldername```
5. Create the dockerfile on the host with ```touch Dockerfile```, then ```nano Dockerfile```, paste our commands and exit nano with ```Ctrl + x```, press ```Y``` to save the file.
6. Run the command ```docker build -t <image-name> .```, this wil create the new image based on the public image ```nginx``` and deploy a simple webpage to the folder.
7. Run your new docker container with ```docker run -d -p 80:80 <image-name>```
8. Now your website should be running, so get the IP from Azure and check that everything is fine.

# Using Azure File Storage

First deploy the Azure Ubuntu with Docker VM from Azure Portal Market Place.
Then using putty connect to your vm and execute the following series of commands to install needed tools.

```
sudo apt-get install -y cifs-utils
git clone https://github.com/Azure/azurefile-dockervolumedriver src/azurefile
export GOPATH=`pwd`
export GO15VENDOREXPERIMENT=1
cd src/azurefile


sudo app-get install golang-go
go get -d github.com/Azure/azure-sdk-for-go/management
go get -d github.com/Sirupsen/logrus
go get -d github.com/ahmetalpbalkan/dkvolume
go get -d github.com/codegangsta/cli

go build -o azurefile
./azurefile -h
sudo ./azurefile --account-name <storagename> --account-key <accesskey>
cd /

#The following command creates the myshare on filestorage and make a local name my_volume
docker volume create --name my_volume -d azurefile -o share=myshare 

```
Now the volume my_volume is ready to use like below:

```

# pull and run ubuntu image with mounted storage to /data
docker run -i -t -v my_volume:/data ubuntu /bin/bash

#inside the container
touch /data/helloworld
exit

#alternative just run it
docker run -v my_volume:/data ubuntu /bin/bash -c "touch /data/helloworld"

```

You can now verify that there is a helloworld file in your myshare on your azure file storage.

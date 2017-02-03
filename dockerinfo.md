https://github.com/docker/kitematic/wiki/Common-Proxy-Issues-&-Fixes

Add Proxy settings to VM

If you have an enterprise proxy between your workstation and the public internet you also need to configure
this proxy in your boot2docker vm host.

Login to the VM via docker-machine ssh default (on windows, it may be easier to connect 
with WinScp to the docker host using DOCKER_HOST IP login user:docker and pwd:tcuser)

Edit the user profile to add the following proxy settings:

sudo vi /var/lib/boot2docker/profile

# Press 'i' to start editing mode
export HTTP_PROXY=http://your.proxy.name:8080
export HTTPS_PROXY=http://your.proxy.name:8080
# Press 'escape' and then type ':x' to save and exit the file. 

Now restart your vm for the above proxy settings to take effect via
docker-machine restart default



docker  images  -q  | xargs docker  rmi
docker ps -a -q  | xargs docker rm

https://www.digitalocean.com/community/tutorials/
 how-to-work-with-docker-data-volumes-on-ubuntu-14-04#learning-the-types-of-docker-data-volumes
 
docker create -v /tmp --name datacontainer ubuntu
docker run -t -i --volumes-from datacontainer ubuntu /bin/bash
echo "I'm not going anywhere" > /tmp/hi
exit
docker run -t -i --volumes-from datacontainer ubuntu /bin/bash
cat /tmp/hi

mkdir ~/nginxlogs
docker run -d -v ~/nginxlogs:/var/log/nginx -p 5000:80 -i nginx


docker create -v /tmp --name datasuse robidock/opensuse 
docker run -t -i --volumes-from -h DATACON datasuse robidock/opensuse   /bin/bash
echo "I'm not going anywhere" > /tmp/hi
exit
docker run -t -i --volumes-from -h DATACON datacsuse robidock/opensuse  /bin/bash
cat /tmp/hi


# docker search mysql
# docker pull mysql
# docker run -e MYSQLROOT_PASSWORD=geheim -p 4242:3306 mysql

# docker pause my_db
# docker run --rm --volume-from my_db  -v /data/backup:/backup  myregistry/foo/dbbackup
# docker unpause my_db

docker export my_db  > my_db.ta


#liefert Liste nicht mehr benötigter Image Fragmente
# docker images -f dangling=true 

#Konsolen-Ausgabe wird von Docker im Verzeichnis 
# /var/lib/docker/containers/<container_id> im JSON-Format abgelegt

#docker run -it --rm --name gustav4 -h gusti robidock/opensuse  /bin/bash

#docker run -it --name vol-test -h CONTAINER -v /data robidock/opensuse  /bin/bash
#  /data  in /var/lib/docker/volumes/<VOLUME>/_data

docker volume create  --name my-vol
docker run -it --rm --name voltest1 -h CONTAIN1 -v my-vol:/mydata robidock/opensuse /bin/bash


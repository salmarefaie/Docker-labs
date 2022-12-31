# Docker-labs

## Lab1

### Problem 1

Run the container hello-world
         sudo docker run hello-world

Check the container status
>         sudo docker ps -a

Start the stopped container
>         sudo docker start 30547b8dc456

Remove the container
>         sudo docker rm 30547b8dc456

Remove the image
>         sudo docker image rm feb5d9fea6a5 

### Problem 2

Run container centos or ubuntu in an interactive mode 
>         sudo docker container run -i ubuntu

Run the following command in the container “echo docker ”
>         Echo docker

Open a bash shell in the container and touch a file named hello-docker
>          sudo docker container run -it ubuntu
>          touch hello-docker

Stop the container and remove it. Write your comment about the file hello-docker
>          sudo docker ps -a
>          Ctrl d
>          sudo docker rm 638ff1a246a2
>          comment about the file hello-docker: Remove file


Remove all stopped containers
>          sudo docker rm $(sudo docker ps -a -q)
>          OR
>          sudo docker container prune

### Problem 3
Run a container httpd with name apache and attach a volume to the container: Volume for containing static html file
>         sudo docker run -it -v volume:/var/www/html --name apache2 httpd bash

Remove the container
>         sudo docker rm 967d975890ce 

Run a new container with the following: Attach the volume that was attached to the
previous container & Map port 80 to port 9898 on you host machine & Access the html files from your browser
>         sudo docker run -it -v volume:/var/www/html -p 9898:80 --name apache3 httpd bash

### Problem 4
Run the image httpd again without attaching any volumes
>         sudo docker run -it -p 9898:80 --name apache4 httpd bash

Add html static files to the container and make sure they are accessible
>         touch file.html

Commit the container with image name my apache
>         sudo docker commit -t "my apache" 82d2630ac341 httpd 

Create a dockerfile for ngnix and build the image from this dockerfile
>         sudo docker build -t image_nginx .
>          In dockerfile:
>               FROM nginx:latest


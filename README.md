# Docker-labs

## Lab1

### Problem 1

Run the container hello-world
>         sudo docker run hello-world

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
>         sudo docker container run -it ubuntu
>         touch hello-docker

Stop the container and remove it. Write your comment about the file hello-docker
>         sudo docker ps -a
>         Ctrl d
>         sudo docker rm 638ff1a246a2
>         comment about the file hello-docker: Remove file


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
>         In dockerfile:
>               FROM nginx:latest

### Problem 5
Create a volume called mysql_data, then deploy a MySQL database called app-database. Use the mysql latest image, and use the -e flag to set MYSQL_ROOT_PASSWORD to P4sSw0rd0!.Mount the mysql_data volume to /var/lib/mysql.The container should run in the background.
>         sudo docker run -d -e MYSQL_ROOT_PASSWORD="P4sSw0rd0!" -v mysql_data:/var/lib/mysql --name app-database mysql





## Lab2

### Problem 1
Create your own nginx docker image based on ubuntu “NEVER USE FROM nginx”
- Install nginx
- Two index.html one as file and another as .tar "/var/www/html"
- Expose
- Start
- Port mapping

>           IN Dockerfile:
>                FROM  ubuntu:22.04
>                RUN apt update
>                RUN apt install nginx -y
>                ADD index.html /var/www/html
>                ADD index_tar.tar.gz /var/www/html
>                EXPOSE 80
>                CMD [ "/usr/sbin/nginx", "-g", "daemon off;" ]


>           IN Terminal:
>                tar -czvf index_tar.tar.gz index_tar
>                sudo docker build -t nginx_image:1.0 .
>                sudo docker images
>                sudo docker run -d -it --name nginx_container -p 8000:80 nginx_image:1.0
>                sudo docker ps -a


### Problem 2
Create react app docker container "using single stage, Multi-Stage Dockerfile"

>           IN Terminal:
>                curl -sL https://deb.nodesource.com/setup_18.x | sudo -E bash -
>                sudo apt-get install -y nodejs
>                npx create-react-app my-app
>                cd my-app
>                touch Dockerfile

>           IN Dockerfile Single Stage:
>                FROM node:alpine3.16
>                WORKDIR /app
>                COPY package*.json ./
>                RUN npm install
>                COPY . .
>                EXPOSE 3000
>                CMD ["npm" , "start"]

>           IN Terminal Single Stage:
>                sudo docker build -t my-app:1.0 .
>                sudo docker run -it --name react_app -p 3001:3000 my-app:1.0    

>           IN Dockerfile Multi Stage:
>                FROM node:alpine3.16 AS build
>                WORKDIR /app
>                COPY package*.json ./
>                RUN npm install
>                COPY . .
>                RUN npm run build
>                # Deploment "nginx"
>                FROM  nginx:alpine
>                COPY --from=build /app/build /usr/share/nginx/html
>                EXPOSE 80
>                CMD [ "nginx", "-g", "daemon off;" ]

>           IN Terminal Multi Stage:
>                sudo docker build -t my-app2:1.0 .
>                sudo docker run -it --name multi -p 8001:80  my-app2:1.0   

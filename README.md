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
          sudo docker container run -it ubuntu
          touch hello-docker

Stop the container and remove it. Write your comment about the file hello-docker
          sudo docker ps -a
          Ctrl d
          sudo docker rm 638ff1a246a2
          comment about the file hello-docker: Remove file


Remove all stopped containers
          sudo docker rm $(sudo docker ps -a -q)
          OR
          sudo docker container prune

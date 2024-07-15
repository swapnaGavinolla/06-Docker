### Docker installation
- use docker_installation.sh file
- after installation exit and login

## docker commands

- docker images    ---> lists images

- docker images -a -q    ---> gives image id's

- docker ps   ---> lists down running containers

- docker ps-a   ---> lists down all containers (running/stopped/created/exited)

- docker ps -a -q   ---> gives container id's

- docker pull &lt;image-name&gt;  -version   ---> downloads the image from local/docker hub

- docker create &lt;image-id&gt;   ---> creates the container

- docker start &lt;container-id&gt;   ---> starts the container

- docker stop &lt;container-id&gt;   ---> stops the container 

- docker run = pull+create+start

- docker run &lt;image-id&gt;  ---> pull+create+starts-->container 

- docker logs &lt;container-id&gt; ---> to checks the logs

- docker inspect &lt;container-id&gt; ---> to inspect container
- docker run debian ping google.com --> to ping

###############################

--use -f to force kill

- use backticks for removal

- docker rmi `` ` ``&lt;image-id&gt;`` ` `` ---> removes image

- docker rmi  `` ` ``&lt;docker images -a -q&gt;`` ` `` ---> removes all images

- docker rm  `` ` ``&lt;container-id&gt;`` ` ``  ---> removes container

- docker rm  `` ` ``&lt;docker ps -a -q&gt;`` ` ``  ---> removes all container

############################

### docker run -d --name &lt;give-name-here -p &lt;host-port:&lt;container-port &lt;image-name:version

#### docker run -d --name mynginx -p 8081:80 nginx:perl

- -d --> detach mode
- --name give-name-here
- -p host-port:container-port 

- docker exec -it container-id bash  ---> login into the container
   
############################

## How to create image ??

### dockerfile --> a declaratice way of creating own images

- build the images and push do docker hub
- bulding the images follow the below instuctions

1. FROM --> to select base OS
    #### FROM &lt;image-name&gt;:&lt;vesrion&gt;

2. RUN --> to install or configure inside base OS
    #### RUN yum install nginx -y 

    - runs at the time of image building --> docker build

3. CMD 
    -  specify default commands 
    -  can override
   #### CMD [ "nginx", "-g" "deamon-off"] 
   - runs at the time of container creation --> docker run  
4. LABEL --> filtering
    - to give metadata
    - key-value pair

    ##### LABEL COURSE=DevOps
    ### `docker images --filter label=COURSE=DevOps`
5. EXPOSE
    - not adding any functionality, just for exporting port
    - to know port --> `inspect` command 
     
     ### EXPOSE 80/tcl

6. ENV
    - to set environment variables
    
7. COPY 
    - copy files and directories 
    - file should be there in local
    ### COPY file-name dest
    ### eg: COPY index.html /usr/share/html/index.html
8. ADD
    - same as COPY and
    1. directly `gets content from internet and copy`
    2. directly `untar the files to the location`

    ADD file-name dest
    ADD link-url dest
    ADD file.tar dest

9. ENTRYPOINT
    - specify default executable
    - can't override
10. USER
    - performs tasks on the name of user
11. WORKDIR 
    - performs tasks inside the directory
12. ARG 
    - supplies variables at the build time
    - ARG can be 1st instruction to supply OS version
    - ARG variable before FROM will not work after FROM
    - 
    

#######

- move into dir where dockerfile exists, then

#  image creation | running | pushing to docker hub | running pushed image

## building image

### docker build -t &lt;image-name&gt;:&lt;version&gt; .

## runnig container

### docker run -d --name &lt;give-name-here -p &lt;host-port&gt;:&lt;container-port&gt; &lt;image-name&gt;:&lt;version&gt; 

[or]

### docker run -d &lt;image-name&gt;:&lt;version&gt;

## login into the container

### docker exec -it &lt;container-id&gt; bash/sh   

### `instead of docker run & docker exac` 
### docker exec -it &lt;image-name&gt;:&lt;version&gt; bash [or] docker exec -it &lt;image-id&gt; bash 

## pushing to docker hub
### docker push docker.io/&lt;username&gt;/&lt;image-name&gt;:&lt;version&gt;
- docker.io is default
- username and image name mandatory
## running pushed image
### docker run -d &lt;username&gt;/&lt;image-name&gt;:&lt;version&gt;

# Docker networking
1. host
2. bridge (default)

### docker network create &lt;network-name&gt;
### docker network ls 
- `before run make sure the image is build`
### docker run -d --name &lt;image-name&gt; --network=&lt;network-name&gt;  &lt;image-name&gt;:&lt;version&gt; 
### eg: docker run -d -name mongodb --network=roboshop mongodb:v1
- launching mongodb into roboshop network

# Docker compose
- install `docker compose` in the instance where we have `docker` installed
- to run docker compose `make sure all images are build`
- files in `.yaml` extension

### docker-compose up -d
### docker-compose down -d

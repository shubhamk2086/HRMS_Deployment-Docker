# HRMS_Deployment-Docker

docker Install-setup
-------------------
 

# Update system
sudo apt update && sudo apt upgrade -y

# Install dependencies
sudo apt install -y ca-certificates curl gnupg lsb-release

# Add Docker GPG key
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# Add Docker repository
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
https://download.docker.com/linux/ubuntu \
$(lsb_release -cs) stable" | \
sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Install Docker
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io \
docker-buildx-plugin docker-compose-plugin
 

# Allow docker without sudo
sudo usermod -aG docker ubuntu
exit

# Start & enable Docker
sudo systemctl start docker
sudo systemctl enable docker
Docker images

Undurstand project Dependency and structute
----------------------------------------------
Backend & Frontend Deployment 
Backend

Framework = spring boot so use java baseing
• Understand / find which language is used in the project.
• pom.xml indicates that Java is used.
• Check the dependency section inside pom.xml.
• Spring Boot is used as the backend framework (defined in pom.xml).
Why Java & Maven are required?
• Spring Boot does not run by itself; it requires two things:
• Java
• Maven
• Without Java, the application is like a car without an engine.
• Java version used: Java 17 (Eclipse Temurin).
Role of Each Tool
• Java – Used to run the Spring Boot application.
• Maven – Used to build the project and download all dependencies.
• Maven creates a JAR file that contains all required dependencies.
• Spring Boot – Backend framework.
Frontend
• Developers use Angular as the frontend framework.
• Angular is built using JavaScript / TypeScript.
• Angular applications run using Node.js.

Frontend

work from = Angular (package.json present inside)

check dist folder bcoz after apth build where
store/output this present in dist folder

If dist not present build this dist bcoz this
path we needs to mention in Dockerfile

After this apth build in dist nginx serv this
on web so dist is imp.

If to not found dist check in angular.json
"outputpath" : "dist"

If not have dist build angular then automatic create dist npm install
npm build run

why dist

web server (nginx) only serve static files which in dist/

without dist nginx not serve apth

when we write Angular apth write in Typescript/HTML/CSS

Browser cannot directly run Typescript they need static
files so after build Angular Typescript convert
into static & store in dist so browser can understand

-> ls -d -> short trick to find dist
service with name same from yml bcoz frontend
forward API to backend & backend connect to SQL
not frontend connect SQL (front depends on backend)
& backend depend on SQL
& same mention at depends section at frontend
block in yml file

<publicIP>:80 -> access APPth
port 80 -> bcoz we access backend & port of
backend is 80 & front depends on backend so
we access backend
In my case not dist so we need build Angular
so need to install npm & build ng build

default.conf
In this file we write backend service name in from yaml
& write this in proxy section under location

-> proxy_pass http://<service-name>:8080;

service with name same from yml bcoz frontend forward API to backend & backend connect to SQL not frontend connect SQL (front depends on backend) & backend depend on SQL & same mention at depends section at frontend block in yml file

<publicIP>:80 -> access APPth
port 80 -> bcoz we access backend & port of
backend is 80 & front depends on backend so
we access backend

-------------------------------------Docker-COMMANDS----------------
- docker images -> check image present or not
-docker ps ->show running container
-docker ps -a -> show all container
- docker  run -it ubuntu /bin/bash  ->docker image install  <ubuntu>
- docker  run -it --name shubham   ubuntu /bin/bash-> creat container
- cat /etc/os-release  ->check which ubuntu,linux run
-docker images->check images on docker
-docker pull jenkins-> only want in docker not run in future we use
 docker search <ubuntu,linux,jenkins> -> whithout go docker hub search 
- docker  run -it --name shubham   ubuntu /bin/bash->chnge container name
-docker start/stop shubham ->start/stop perticular container
-docker attach shubham->go in container
- docker rm shubham->delete container->1st stop then delete->when exit automatic stop

*3 ways to make img

How to create container to image image to container
------------------------------------------------------
*How to create container -:-
-------------------------
1)-docker run --name shubham -it ubuntu/bin/bash->create container with name
-ls->cd tmp->touch<create file> ->afer made container made  img from this container 


*made image from container
---------------------------
docker commit <container name> updateimg

* again made container from  image-
--------------------------------
- docker  run -it --name shubham   ubuntu /bin/bash ->create container 

*how to make vi file for docker-
vi Docker 
---------

FROM ubuntu
WORKDIR /tmp->where we want work 
RUN echo "Jay Shri Ram" > /temp/testfile  ->what print in docker file
ENV myname shubham_kumbhar -> what who chnge 
COPY testfile /tmp-> copy file from container
ADD test.tar.gz /tmp-> copy from docker ub

* make imge from Docker file
---------------------------------
-docker build -t test . -> build img from Dockerfile 

*Make container from from img
--------------------------------
- docker  run -it --name shubham   ubuntu /bin/bash

----------------------------------------------------------
*create volume
-------------
1)make docker file
vi Dockerfile
FROM ubuntu
VOLUME ["/volume-file-name"]
:wq

2)-docker build -t <imgename> -> make img from docker file
3)-docker  run -it --name shubham   <img name>/bin/bash ->create contner
4)-docker  run -it --name cont2 --privileged=true --volumes-from cont1 ubuntu /bin/bash->share volume of cont1 to cont2

* create volume by using command
---------------------------------
- docker run -it --name hostcont -v /home/ec2-user:/skk --privileged ubuntu /bin/bash->connect host to cont
-










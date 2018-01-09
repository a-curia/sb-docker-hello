SpringBoot and Docker
---------------------

 

Dockerfile should contain:

step1: chose the java image

*FROM openjdk:8*

step2: add the project jar location to docker container root location

*ADD target/spring-boot-docker.jar spring-boot-docker.jar*

step3: expose port to the docker container

*EXPOSE 8080*

step4: specify which is the command to run the jar

*ENTRYPOINT ["java","-jar","spring-boot-docker.jar"]*

 

To create the docker image go to project root directory and do the following:

**docker build -f Dockerfile -t spring-boot-docker .**

 

-   display all docker images:

\$ docker images

-   run the image and map the ports between docker container and application
    container

\$ docker run -p 8085:8080 spring-boot-docker

 

If you have an application that needs persistence container like MySQL, you can
use **--link** to ling the microservice with the persistence, and on the
application.properties, instead of the localhost mysql address, use the
persistence container name.

 
Docker and MySQL

- pull the image and create the container with specific user and password
$ docker run -p 3306:3306 --name mysqlserver -e MYSQL_ROOT_PASSWORD=password -d mysql:latest

OR

- pull the latest image
$ docker pull mysql/mysql-server:latest
- deploy the container
$ docker run --name=mysql01 -d mysql/mysql-server:latest
- get the default password
$ docker logs mysql01
- change the password with the desired password
$ docker exec -it mysql01 mysql -uroot -p
mysql# ALTER USER 'root'@'localhost' IDENTIFIED BY 'newpassword';
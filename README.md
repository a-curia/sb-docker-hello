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

 

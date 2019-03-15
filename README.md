# bp-deploy

BUILD 
clone 4 repos
1) frontend
  - main page 
     - do nothing
  - microservice UI
    - run npm run build
  - springhibernate UI
    - run npm run build
2) microservice
  - run mvn install and upload jar
3) springhibernate
  - run mvn install and upload jar
4) pythonservice
  - run 
  
DEPLOY
1) frontend
  - stop current container
  - delete current container
  - delete current image
  - docker build with dockerfile
    - use nginx image
    - copy main page to nginx docroot
    - create springhibernate folder
    - copy content of build folder to this folder
    - create microservice folder
    - copy content of build folder to this folder
  - start docker on port 80:80
  - run inspec test
  - if good upload docker image to docker hub
2) microservice
  - stop current container
  - delete current container
  - delete current image
  - docker build with dockerfile
    - use openjdk:8-jdk-alpine image
    - copy jar to root
  - docker run -d -p 8080:8080 -e SA_LOGIC_API_URL='http://<container_ip or docker machine ip>:5050' $DOCKER_USER_ID/bp-microservice
  - run inspec test on healthCheck api
  - if good upload docker image to docker hub
3) springhibernate
  - stop current container
  - delete current container
  - delete current image
  - docker build with dockerfile
    - use openjdk:8-jdk-alpine image
    - copy jar to root
  - start docker on port 9090:8080
  - run inspec test on healthCheck api
  - if good upload docker image to docker hub
4) pythonservice
  - stop current container
  - delete current container
  - delete current image
  - docker build with dockerfile
    - use python:3.6.6-alpine
    - copy rs folder to /app
    - set /app as working dir
    - run pip3 isntall
    - run python file
  - start docker on port 5050:5000
  - run inspec test on reverse_sentence api
  - if good upload docker image to docker hub
  5) Run end to end test
  
  DEPLOY from dockerhub
  1) frontend
  - stop current container
  - delete current container
  - delete current image
  - docker pull
  - start docker on port 80:80
  - run inspec test
  - if good upload docker image to docker hub
2) microservice
  - stop current container
  - delete current container
  - delete current image
  - docker pull
  - docker run -d -p 8080:8080 -e SA_LOGIC_API_URL='http://<container_ip or docker machine ip>:5050' $DOCKER_USER_ID/bp-microservice
  - run inspec test on healthCheck api
  - if good upload docker image to docker hub
3) springhibernate
  - stop current container
  - delete current container
  - delete current image
  - docker pull
  - start docker on port 9090:8080
  - run inspec test on healthCheck api
  - if good upload docker image to docker hub
4) pythonservice
  - stop current container
  - delete current container
  - delete current image
  - docker pull
  - start docker on port 5050:5000
  - run inspec test on reverse_sentence api
  - if good upload docker image to docker hub
  5) Run end to end test

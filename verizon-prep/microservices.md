

# Microservice Questions

## Microservices
- Microservices areautomous, independently, deployable services collaborate together to form a broader application

## Why we need microservices
- Horizontal scale
- Spererate services that easier to update, manage

##  Compare the microservice and monolithic architectures. What are the advantages / disadvantages of each?
## Monoliths: 
- Single codebase, Single process Single host, Single database, Consistent technology
- **Benefit**: 
	- Simple, one codebase- easy to find, for deployment, there's only 1 application to update. 
	- It Works well for small app, with a small dev team (2-3 members), work together for a few months, moderate visitors
- **Problem**: its scale. 
	- When codebase become big, it is very difficute to deploy: Even one small change requires downtime and break the code
	- Really difficult to scale: unable to scale horizontally and vertical scalling are expensive. Plus, the entire application have to be scalled together
	- Hard to get away from legacy code since we have to move the entire application to a new framework
## Microservices:
- Benefit:
	- Contains small services that can be owned by small development team. A rule of thumb is it should be small enough to be throw away and rewritten in a different way
	- Able to adopt new technology without the need to update anything in one go. We can choose the right tool for the job
- Ability to deploy them individually which minimize downtime and reduce risk enable frequent updates
	- Scaling: scale the services individually
	- The services can be reuse
- Challenges:
	- Difficult to define Microservices boundaries (Domain Driven Design)
	- Complex interaction (auto deployment workflow like Docker)
	- Operation Insight (centralize logs)
	- Overtime some microservices maybe bloated (check regulary)

## Distributed Monolith
- **Architechure base services** Have several services that run to different host and talk to each other over a network
- Have an architechture base services doesn't mean it not monolith. It can uses a shared database and tightly coupled to each other in a way we have to deploy them all together and all changes in the system we made required multiple services. They are often refferred as distributed monoliths. They combine all the downsize of monoliths with all challenges of microservices
- So better understand micro services very well before creating them or we could end up in a world of pain

##  How do you solve the different problems inherent to microservices?
- If not careful, a microservice can become a distribute monolith which consist of all disadvantage from both

##  What are the difference between a MSA and a SOA?
- Service-oriented architecture (SOA) is an architectural pattern as well as a collection of design principles that support loose coupling and reusability of different components
- An SOA architecture recognizes that within an application these components are required, and creates a structure where the components themselves can exist independent of each other
- Service-oriented architecture is often compared to microservices as both share the same fundamentals. Microservices, which are more recently developed than SOA, are even considered to be a type of SOA
SOA | Web service
---- | ----
create reusable service | continuous interation and delivery is key
older | new
access common data store | each microservice has its own data repository (self-contained)

##  Can a Java microservice communicate with a Node.js microservice? Why or why not?
- Yes. Because they can send and retrieve information from the same communication protocol

## Synchronous and Asynchronous communication
## Syncronous: 
- HTTP -> Clients send a request and wait for a response. Other code will not execute until the request sent back. Easy code, most suitable in most case, long response time, not good user experience
- Ex: User order something, goes to productService, send back, goes to PaymentService, Send back data, go to mailing service, send back data, go to analytic service, send back data, response to the user. User actually doesn't have to wait for mailing and analytic service
## Asynchronous: 
- AMQP  -> Other code can still be excecute while waiting for a response. Reduce dependencies between services. Scale easier, event driven. In asynch, the services will consume resources even if the services aren't in use
- Ex: User order something, goes to productService, send back, goes to PaymentService, Send back data, send message to the user. Then go to a Message Broker, which will handle 2 request at the same time
- Asynchronuous communication options:
	- Event based: message broker, Queuing Pattern:
		- RabitMQ Message Broker (terminal)
	- Async API calls: request achknowelege using callback 
## API architechture style recommended
- Pragmatic REST (extended unoffical version of Rest, not all about CRUD, ation/task based endpoints)
- HATEOAS (true REST) 
	- When get a REST call, not only get the data but also the action link the the user can take. We can create those link dynamicly in Spring Boot and Spring using Hateoas project to implement it
	Ex: withdraw -200, send a deposit link
```java
@GetMapping("/account/{id}")
public ResponseEntity<?> getAccountDetail(@PathVariable Long id){
	ResponseEnitity<?> responseEntity = accountService.findOne(id);
	SuccessResponse success = (SuccessResponse) responseEntity.getBody();
	Account account = (Account) success.getObject();

	EntityModel<Account> resource = EntityModel.of(account)
	resource.add(WebMvcLinkBuilder.linkTo(WebMvcLinkBuilder.methodOn(this.getClass()).deposit(new Account())).withRel("deposit))
	return new ResponseEntity<>(resource, HttpStatus.OK)
}
@PutMapping("/deposit")
public ResponseEntity<?> deposit(@RequestBody Account account){
	return accountService.depositToAccount(account);
}
```
```java
Link link = linkTo(CustomerController.class).withSelfRel();
CollectionModel<Customer> result = CollectionModel.of(allCustomers, link)
return result;

// http://localhost:8080/spring-security-rest/api/customers

linkTo(CustomerController.class).slash(customer.getCustomerId()).withSelfRel();

// http://localhost:8080/spring-security-rest/api/customers/30C
```
- RPC
- SOAP

## Compose Microservices together
- Broker Composition Pattern (Message broker, asynchronus)
- Aggregate Composition Pattern (a service that control other services)
- Chained Composition Pattern (synchronuous, delay responsiveness, able to use other patterns to split the chain )
- Proxy Composition Pattern (Gateway API, all the request go here and it forward to other services)
- Batch/Branch Composition Pattern (useful when need different type of behaviour for eacch part. Aggregator will split the request to different services. Ex: Task split into 2 services. service OneA uses Chain Composition since it needs something from service OneB, service Two use Message Composition Pattern to perform task asynchronuously)

## Microservices vs REST
Loosely coupled, Independently changeable + deployable, stateless, 
Microservices | REST
-------- | ------
Architechture type | Architechture type

## Serverless Computing
- Deploy function instead of application
- Scale quickly, start fast, run short
- Run code without knowlege of infrastructure

5.  What are the difference between horizontal and vertical scalability? Which way do monoliths and microservices typically scale?

##  What are some best practices for building microservices?
- Centralized loging, tracing to know the all services that the request go through  (Zipkin and Sleuth)
- Boundary Context (domain driven design)
- Automated deployment (or else it'll be error prone, time consuming and painful)
- Configuration management through a centralize service
- Better to use a standard tech stack. Single tech stack is ok. Lots of tech stack makes support extremely painful, limits movement between teams
- Circuit breakers, health checks, test
- Best practices is to use a message queue for asynchronus call so if 1 service break, other services can still run

## Zipkin and Sleuth
- Centralized micro service logging
- zipkin.o/pages/quickstart.html
- Download Zipkin by Java latest release(.jar) (or docker)
- cmd, type java command ```java -jar zipkin-server-2.21.7-exec.jar```
- Copy the url (+ "/zipkin") and try it on browser
- Add spring cloud zipkin and sleuth dependencies to services like user and department services
- Add zipkin url to those services
```yml
spring:
	application:
		name: DEPARTMENT-SERVICE
	zipkin:
		base-url: http://127.0.0.1:9411/
```

## Spring Cloud Task
- Short-lived, asynchronus microservices

##  How large should each service in a microservice be?


##  What is a messaging queue and how is using one different from calling service APIs directly?
- A message queue is a form of asynchronous service-to-service communication used in microservices architectures
- There's AMQP(Advanced message Queuing Protocol) via RabbitMQ that can be used in Spring
- Event bus (publish, subcribe channel) (RabbitMQ, Azure Service Bus)

9.  Explain the Netflix OSS stack for microservices (Eureka, Zuul, Hystrix)

10.  How would you setup and configure Eureka? Zuul? Hystrix?

##  What is the purpose of an API gateway and how does Zuul perform this?
- Minimize API surface that we exposing publicly and gives us a single point of entry to protect

12.  What is service discovery and how does Eureka do this (we used Consul)?

13.  What is the circuit breaker pattern and how does Hystrix implement it?
<br>

![Happy Christmas](VyNotes/microService/API-gateway.jpg)
![Happy Christmas](VyNotes/microService/cloud-config1.jpg)
![Happy Christmas](VyNotes/microService/cloud-config2.jpg)
![Happy Christmas](VyNotes/microService/cloud-config3.jpg)  


# CI/CD
## What is CI
- Continous Integration is a development practice that requires developers to integrate code into a shared repository serveral times a day. Results in a deployable release
- Principles:
	- Have a single place where the code live
	- Everyone commits to the mainline everyday
	- Automate the build process
	- Every commit triggers a build
	- Automate testing process
	- Everyone had access to the latest
- Benefit:
	- Integration takes less effort
	- Issues will come up more early
	- Automation means less issues
	- The process is more visible
- Faster delivery, lower costs, more flexible
- How to CI:
	- Get to a single source Control Repository: Often there just 1 main branch with some hotfix branch. No feature branches.  Clean hotfix daily, merge them to main branch. Collaboration frequently. Know what other team doing all the time
	- Automated Build process. Need 1 server specificly to the code. Install a build engine. Create build definition
	- Create an Automated Test process: run static tests with the build. (Optional) Deploy the built result to a temporary environment. Run UI test

## What is CD
- Continous delivery is a software developement discipline where software can be released to production at anytime
- Need continuous Intergration to Continuous Deployment
- CD principles:
	- Have continuos intergration in place
	- Automate the environment creation process
	- Automate the release process
	- Releasing on-demand
	- Anyone had access to the latest result
- Benefit:
	- Automatic so less error, less effort
	- Releasing is more Reliable, repeatable
	- Release more often
	- Get feedback earlier
- How to CD:
	- Have Continuous Integration in place
	- Unite developers and operations (devop)
	- Create a release pipeline: configure a deployment server, create release definition (scripting deployment of software, update schema, copy file to server),run tests. (Optional) create an Infrastructor as code Process: scripts environments (json format, Powershell format)
## Continous Delivery vs Deployment
Continuous Delivery | Continuous Deployment
----- | -----
Software can be deployed to production at anytime | Software is automatically deployed to production all the time

### SOAP Questions ⁉️

14.  What does the acronym SOAP stand for?

15.  What protocols and data format do SOAP services use?

16.  What is the “contract” for a SOAP service?

17.  What’s the structure of a SOAP message?

18.  What are the SOAP messaging modes? Messaging Exchange Patterns?

19.  Are SOAP messages delivered with GET or POST requests?
<br>
    
### REST Questions ⁉️

20.  What does the acronym REST stand for? What makes a service “RESTful”?  

21.  What protocols and data format do REST services use?  

22.  What are the architectural constraints of REST?  

23.  What is a “resource” in a REST service?  

24.  What does the “uniform interface” constraint mean? Give an example of some RESTful endpoints you would create for an API. Should the URLs contain nouns, verbs, or adjectives?    
<br>

## Docker Questions ⁉️
*Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly.*

> [Here](https://github.com/210222-reston-java-msa/demos/blob/main/week6/docker.md) are the notes and guide on Docker
<br>

## Docker command
```docker
docker --version
docker images --help
docker container --help
```

After pull, list the images
```
docker pull <image-name>
docker images -a
```
```
docker images (all images we have locally)
docker run -p 9092:9091 <Image-name>(or id) 
(9092: local port, 9091: contain port)
open localhost 9092 to look at the app

```
```
docker ps (look at the running containers)
docker ps -a (list active and unactive containers)

docker inspect <image-id>

docker log <container-name | container-id>

docker stop <container>
docker kill <container> 
docker strart <container>
```
Execute a command in the container. After enter, the terminal change to bash command. We can write any bash command there
```
docker exec -it <container> bash 

Save container as image
docker commit <container> <image | new image name>

export container to a tar file
docker export --output <image>.tar <container>

docker import <image>.tar <container>/<new image name>

docker login -u <username> -p <password>
docker push
```
Docker file
```
FROM ubuntu
RUN apt-get update
CMD ["echo","Image created"]
```
Create an image from a docker file
The reason . works is because we cd to DOCKERFILE
```
docker build -t <Repo_tag> <file | . >

docker rm <multiple container id>
docker rmi <image>

Create server. -d : start server in detach mode
docker-compose -f <yml file> up -d

Turn server off
docker-compose -f <yml file> down
```
1.  What is containerization?
    
2.  What is the Docker Daemon?
    
3.  How are containers different from virtual machines? What makes docker containers more lightweight than virtual machines?
    
4.  What is a Docker image? Container?
    
  How is a Docker image different from a Docker container? How are the read/write layers different?
- A Docker image is a read-only, inert template that comes with instructions for deploying containers. A Docker image is made up of multiple layers.
-  Docker image as a recipe and a container as the cake baker from that recipe
Docker Image | Docker Container
------ | ------
Container blueprint | Image instance
immutable | Writable
Can exist without a cointainer | Must run an image to exist
Can be shared | It's already running, no need to share
Create only one | Can create multiple cointainer from the same image
    
6.  List the steps to start Docker, create a Docker image, and spin up a container.
- Create a Docker File at the root
```
FROM ubuntu:20.04
RUN apt update
```
    
7.  What is the relevance of the Dockerfile to this process? List some keywords in the Dockerfile.
    
8.  What is the benefit to an image being built in Layers?
    
9.  What are some other Docker commands?
    
10.  What is a container registry? How would you retrieve and upload images to DockerHub?
    
11.  What is Docker compose and why is it useful?
    
12.  If you want to store state for a container, how does Docker recommend doing that?
```docker run -v <volume_name>:<container_directory> <image_name>```


# AWS
## Deploy SpringBoot to AWS EC2 using S3
- Spring Boot app ```mvn clean install```
- EC2 -> Running Instance -> Launch Instance -> select Instance type -> Launch -> Key pair: AWS_AMI_instance_1 -> Launch -> top: connect -> Standalone SSH client -> connect using PuTTY -> PuTTY Load AWS Instance 1 Hostname: ec2-user@ec2...amazonaws.com -> SSH -> Auth : browse private key -> install java same version as our SpringBoot app
- Create S3 Bucket -> remove block all public access -> tick achknowlede -> create bucket -> create folder-> upload -> our maven exported Snapshot .jar file -> success -> copy object url -> make public
- PuTTY -> in root directory -> wget paste url -> ls to check if jar file there -> java -jar downloaded..SNAPSHOT.jar
- EC2 -> security group -> inbound -> anywhere -> go to instance -> copy Public DNS url -> paste -> page runs

# Jenkin
https://anoni.sh/jenkins-pipeline
- Jenkin gets the latest code from github, build Artifacts (web, app), run tests, publish Output to live server, know if there's any error

## What is Jenkin
- Jenkins is a free automation server written in Java. It helps automate the parts of software development related to building, testing, and deploying, for us to achive continuous integration and continuous delivery. It is a server-based system that runs in servlet containers such as Apache Tomcat

## Freestyle Jobs vs Scripted Pipeline
Freestyle Jobs | Scripted Pip
------ | -------
Configure through GUI | Configure through code
Changes not tracked | Changes tracked (through SCM)
Need to recreate jobs to migrate | Easy to import/export
Need separate jobs for each step in the pipeline | Pipeline can be parameterlized and reuse
Creating and configuring is manual | Creating and configuring is automatically generate

## Pipeline
- A series of tasks required to be build and deploy an application. Start to finished process from source control to production

## Agent
- Defines which Jenkin build agent run the pipeline
- Ex: Have an app we want to build in WIndow and Linux, we have an agent for each of those

## Stage
- A section of the pipeline (Build, test)

## Step
- Specific instruction withing a stage

## Start jenkin for the 1st time
- Download jenkin (jenkins.io, LTS release)
- Place the war file to any location. Open command prompt right there ```java -jar jenkins.war```
- Copy the password and keep it save
- Go to browser - localhost:8080, paste the password
- Select plugin to install or none
- Create user or continue as admin

## Setup Jenkin pipeline
- Github -> Profile -> Developer settings -> personal access token -> generate a new token : Jenkin -> check: repo, admin:repo_hook -> generate token (save it)
- Go to Jenkin -> manage Jenkin -> add Github server -> Credentials -> GitHub Connection -> add -> Jenkin -> Kind: Secret Text -> Secret: our git token , ID: random name -> Add
- Jenkin -> install Pipeline plugin (A suit of pipeline that lets you orchestrate automation, simple or complex)
- Create a Scripted **pipeline (Jenkinsfile)** (1 stage fail, others won't run):
	- Create new jobs (main page) -> write a name -> choose Pipeline
	- Definition: Pipeline -> hello world demo. Left -> blue circle -> console output (option 1)

	- Create new jobs (main page) -> write a name -> choose Pipeline name it-> In the new pipeline, General -> Github project: github url that had Jenkinsfile
	- Definition: choose Pipeline script from SCM -> SCM : Git -> repository: git url -> branch: */master

## Setup Jenkin pipelin
- Create a Jenin token in Github
- Type the token in Jenkin when create a new project
- Install scripted pipeline plugin
- Create a new job, link to a Github repo. Choose to create Pipeline from Script or create in the textarea

## Multibranch Pipeline
- Create a new job, choose Multibranch pipeline instead of Pipeline. In multibranch, it had all the branches in Github

## Jenkin Unit Tests
pwsh = power shell script
```jenkin
pipeline {
	agent any
	stages {
		stage ('Verify Branch'){
			steps {
				echo "$GIT_BRANCH"
			}
		}
		stage ('Docker Build'){
			steps {
				pwsh(script: 'docker images -a')
				pwsh("""
					cd azure-vote/
					docker images -a
					docker build -t jenkins-pipeline .
					cd ..
				""")
			}
		}
		stage ('Start test app'){
			steps {
				pwsh(script: """
					docker-compose up -d
					./scripts/test_container.ps1
				""")
			}
			# This is Post step
			post {
				success {	
					echo "App started successfully";
				}
				failure {
					echo "App failed to start"
				}
			}
		}
		stage ('Run Tests') {
			steps {
				pwsh(script: """ 
					pytest ./tests/test_sample.py
				""")
			}
		}
		stage ('Stop test app'){
			steps {
				pwsh(scripts:""" 
					docker-compose down
				""")
			}
		}

		# --- Add branches
		stage ('Runs on master'){
			when {branch 'master'}
			steps {
				echo 'Hello World'
			}
		}

		# --- Input step, Install Azure Container. Google Kubernetes plugin
		# Click on project name -> Pipeline syntax 
		# Create Azure service to fill in the Pipeline syntax form. Config file **/*.yaml
		
		stage('Run Trivy') {
			steps { sleep (time:30, unit:'SECONDS')}
		}
		stage('Deploy to QA'){
			environment { ENVIRONMENT = 'qa'}
			steps {
				echo "Deploting to ${ENVIRONMWNT}"
				acsDeploy(
					azureCredentalsId: "azure-jenkins-app",
					configFilePaths: "**/*.yaml",
					containerServie: "${ENVIRONMENT}-demo-cluster | AKS",
					resourceGroupName: "${ENVIRONMENT}-demo",
					sshVredentialsId: ""
				)
			}
		}
		stage ('Approve PROD Deploy'){
			when {
				branch 'master'
			}
			options { timeout(time:1, unit: 'HOURS')}
			steps {
				input message: "Deploy?"
			}
			post {
				success {echo "Production Deploy Approved"}
				aborted {echo "Production Deploy Denied"}
			}
		}
	}
}

# Hit Build Now
```



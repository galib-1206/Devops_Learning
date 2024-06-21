# DevOps_Learning

# Level 101
## 1.Fundemantal Series
## **_Linux Basics_
This course is divided into three parts. In the first part, we cover the fundamentals of Linux operating systems.
In the second part, we cover some basic commands used in Linux like navigating the file system, viewing and manipulating files, I/O redirection etc.
In the third part, we cover Linux system administration. 

### Commands for Navigating the File System:

- ls  (list files and directories)
- pwd  (print working directory)
- cd  (change direcotry)


### Commands for Manipulating Files : 

- touch (create new file)
- mkdir (create new directories)
- rm (delete files and directories)
- cp (copy files and directories)
- mv (move files and directories) 
   Eg: mv <source_path> <destination_path>

### Commands for Viewing Files :
- cat (most simplest use to print the contents of the file on your output screen)
- head (displays the first 10 lines of the file by default)
- tail
- more (all)
- less

### Echo Command in Linux
 prints the given input string on the screen.

### Text Processing Commands
- grep (display all the lines in a file that contains a particular input)
 Eg:grep <word_to_search> <file_name>

- sed (used to replace a text in a file)
 Eg:sed 's/<text_to_replace>/<replacement_text>/' <file_name>

- sort 
 increasing order
 lexicographical order

### I/O Redirection
We can use some special operators to redirect the output of the command to files or even to the input of other commands.
  Eg: https://linkedin.github.io/school-of-sre/level101/linux_basics/images/linux/commands/image30.png
 
 ls > redirected file
### Linux Server Administration



## **_Linux Networking Fundamentals_
### OSI Model
Application Layer
Presentation Layer
Session Layer
Transport layer
Network Layer
Data Link Layer
Physical Layer

** Application Layer :
provides services for network applications:
http
https
smtp

**Presentation Layer:
- Translation into Binary form  (ASCII->EBCDIC)
- Data compression
- Data Transmission: Encryption/Decryption ->SSL(secure sockets layer)

**Session Layer:
- Authentication
- Authorization
- Session Management (keep tracking which data packets belongs to textfile or imagefile)
Transport layer

**Transport layer:
- Segmentation
Data receives from session layer devides into **Segments**
Segements having data unit (port num, seq num)
seq num:reassembles data unit for correct connection
 - Flow Control: server to application download speed management
 - Eror Control:Using **Checksum** to retreive missing/corruped data
 **TCP** -Connection Oriented Transmission
**UDP** - Connectionless (no loss data retrieving)

**Network Layer:
- Logical Addressing : IP address
- Routing-  packet goes to Network1 to Network2 by Ip address+ Mask Value checkng which is done by server .
- Path determination: best Possible path
 OSPF(open shortest path first)
BGP(Border Gateway Protocol)
IS-IS(Intermediate system)

**Data Link Layer:
- Pyhsical Addressing : MAC addressing attched  to previously logical Address(IP). its 12 digit alpha-numeric number embedded in NIC (Network interface Card).
- Head, Tail, Frame
- Access Media
**Physical Layer:
- Converts Binary seq into signal and transmits over local media


### Birds eye view of the course
The course covers the question “What happens when you open linkedin.com in your browser?” The course follows the flow of TCP/IP stack.More specifically, the course covers topics of Application layer protocols DNS and HTTP, transport layer protocols UDP and TCP, networking layer protocol IP and Data Link Layer protocol

### DNS
DNS is an **application layer** protocol
#### DNS Resolution : 
When somebody tries to open www.linkedin.com in the browser, the browser tries to convert www.linkedin.com to an IP Address. This process is called DNS resolution. 
The browser would have a DNS cache of its own where it checks if there is a mapping for the domainName to an IP Address already available, in which case the browser uses that IP address. 
If no such mapping exists, the browser calls gethostbyname syscall to ask the operating system to find the IP address for the given domainName

### UDP
UDP is a **transport layer** protocol.

**Multiplexing**:
When a client makes a DNS request, after filling the necessary application payload, it passes the payload to the kernel via **sendto system call**.

The kernel picks a random port number(>1024) as source port number and puts 53 as destination port number and sends the packet to lower layers. 

When the kernel on server side receives the packet, it checks the port number and queues the packet to the application buffer of the DNS server process which makes a **recvfrom system call** and reads the packet.

This process by the kernel is called multiplexing(combining packets from multiple applications to same lower layers).
**Demultiplexing** :
Segregating packets from single lower layer to multiple applications.

### TCP
Another common transport layer protocol **TCP** does a bunch of other things like 
- reliable communication
- flow control
- congestion control. 

But UDP is designed to be lightweight and handle communications with little overhead. 
##### Reliable Connection:
 A TCP connection is established by a three way handshake.
 1. the client sends a SYN packet along with the starting sequence number it plans to use.
 2. the server acknowledges the SYN packet and sends a SYN with its sequence number.
 3. Once the client acknowledges the syn packet, the connection is established.
 
##### Congestion Control:
TCP also does congestion control which determines how many segments can be in transit without an ack.
### HTTP
The HTML page of linkedin.com is served by HTTP protocol which the browser renders.
Browser sends a HTTP request to the IP of the server determined above. Request has a verb GET, PUT, POST followed by a path and query parameters 

### IP Routing and Data Link Layer
When the packet reaches the IP layer, the transport layer populates source port, destination port.

IP/Network layer populates destination IP(discovered from DNS) and then looks up the route to the destination IP on the routing table.

## 2.Python and Web
**What is the difference then, between java and python?**
Java's compiler is more strict and sophisticated.It is a statically typed language. So the compiler is written in a way that it can verify types related errors during compile time.
While python being a dynamic language, types are not known until a program is run. So in a way, python compiler is dumb (or, less strict). 

Python, on the other hand, is an interpreted language. When you run a Python script, it goes through a two-step process:
- **Compilation to Bytecode**: The Python source code is first compiled into bytecode. Bytecode is an intermediate representation that is platform-independent and is not directly executed by the CPU.

- **Execution by Python Virtual Machine (VM)**: The Python bytecode is then executed by the Python interpreter or Python Virtual Machine (VM). The Python interpreter reads the bytecode and translates it into machine code on the fly. This introduces an additional layer of abstraction compared to languages like C or C++.

**in case of C/C++, the output is machine code which can be directly read by your operating system. When you execute that program, your OS will know how exactly to run it. But this is not the case with bytecode.**

##### **Advantages**:
- **Portability**: Bytecode is platform-independent, allowing Python code to be executed on any system with a compatible Python interpreter.

- **Dynamic Typing**: Python's dynamic typing and features like introspection are made possible by the interpretation of bytecode during runtime.

## **_Python Concepts_
- **Everything in Python is an object.**
- That includes the functions, lists, dicts, classes, modules, a running function (instance of function definition), everything. In the CPython, it would mean there is an underlying struct variable for each object.

In python's current execution context, all the variables are stored in a dict. It'd be a string to object mapping.

 ``` sh 
 float_number=42.0
 def foo_func():
 pass
```

**NOTICE HOW VARIABLE NAMES ARE STRINGS stored in a dict
```sh
locals ()
    {'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <class '_frozen_importlib.BuiltinImporter'>, '__spec__': None, '__annotations__': {}, '__builtins__': <module 'builtins' (built-in)>, 'float_number': 42.0, 'foo_func': <function foo_func at 0x1055847a0>}
```
### Decorators
In Python, decorators are a powerful and flexible way to **modify or extend the behavior of functions or methods without changing their source code directly.** 
Decorators are often used for tasks like **logging, authentication, caching, and more.** Decorators are applied using the @decorator_name syntax.

Function Decorators:

- A decorator in Python is essentially a function that takes another function as an argument and adds or modifies its behavior.
- You can define a decorator using the @decorator_name syntax above the function you want to decorate.

**python source code**

```sh def my_decorator(func):
    def wrapper():
        print("Something is happening before the function is called.")
        func()
        print("Something is happening after the function is called.")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")
say_hello() 
```
**Output**:
Something is happening before the function is called.
Hello!
Something is happening after the function is called.

### Sockets


#### **How a python program is executed??**

The execution of the Python program involves 2 Steps:
- Compilation
- Interpreter

#### Compilation
The program is converted into **byte code**. Byte code is a fixed set of instructions that represent arithmetic, comparison, memory operations, etc. It can run on any operating system and hardware. The byte code instructions are created in the .pyc file. The .pyc file is not explicitly created as Python handles it internally but it can be viewed with the following command:

![alt text](https://media.geeksforgeeks.org/wp-content/uploads/20200703191624/binary.PNG)

The dis command is known as “disassembler” that displays the byte code in an understandable format.

#### Interpreter
The next step involves converting the byte code (.pyc file) into machine code. This step is necessary as the computer can understand only machine code (binary code). Python Virtual Machine (PVM) first understands the operating system and processor in the computer and then converts it into machine code. Further, these machine code instructions are executed by processor and the results are displayed.
![alt text](https://media.geeksforgeeks.org/wp-content/uploads/20200703190408/Capture.PNG)
#### **How's python3 is superior than python2.7 ?**
**Unicode Support**:
Python 3 has native support for Unicode, making it the default string type. In Python 2.7, strings were ASCII by default, and Unicode support required explicit handling with the u prefix.

**Print Function**:
Python 3 uses the print() function instead of the print statement, providing a more consistent and versatile way to print output. This change makes it easier to adapt to various output requirements.

**Division Behavior**:
Python 3 changes the division operator behavior, making the / operator always perform true division. In Python 2.7, division between two integers resulted in integer division unless one of the operands was a float.

**Syntax Improvements**:
Python 3 introduced syntax improvements to enhance readability and consistency, such as the removal of redundant constructs and adjustments to function annotations.

**Range Function**:
The range() function in Python 3 returns an iterator, similar to the behavior of xrange() in Python 2.7. This change improves memory efficiency when dealing with large ranges.

**Modern Language Design**:
Python 3 incorporates lessons learned from the development of Python 2 and strives for a more consistent and clean language design. It eliminates certain inconsistencies and improves the overall structure of the language.

**Enhanced Libraries**:
Some Python 3 features and improvements are library-specific, providing enhanced functionality and better performance. New modules and features have been added to the standard library.

**Easier Porting to Future Versions**:
Python 3 is designed to be forward-compatible, making it easier for developers to port their code to future versions of the language. The Python community actively encourages migration to the latest Python 3 release.

**Example**: https://www.mygreatlearning.com/blog/python-2-vs-python-3/




# Level 102
## 1.Linux Intermediate
## **_Package Management_
Package management is a method of installing and maintaining software programs on any operating system

 Package file is a **compressed collection** of files that contains software, its dependencies, installation instructions and metadata about the package.
 ### Repository
 Repository is a storage location where all the packages, updates, dependencies are stored. 
 Each repository can contain thousands of software packages hosted on a remote server intended to be installed and updated on linux systems. 
 We usually update the package information ( often referred to as metadata) by running “sudo dnf update”.
 
Linux Distribution ->	Low-Level |	High-Level 
Debian ->	        dpkg	|      apt-get
Fedora,RedHat ->	dnf	    |       dnf

## **_Storage Media_
Storage media are devices which are used to store data and information. Linux has amazing capabilities when it comes to handling external devices including storage devices. There are many kinds of storage devices physical storage devices like hard drives, virtual storage devices like RAID or LVM, network storage and so on.

## **_Archiving and Backup_
### Archiving
We usually archive the data that are no longer needed but are kept mostly for compliance purposes. This helps in storing the data into compressed format saving a lot of space. Below section is to familiarize with the archiving tools and commands.

#### gzip
gzip is a program used to compress one or more files, it replaces the original file with a compressed version of the original file.

### Backup
Backup is a process of copying/duplicating the existing data, This backup can be used to restore the dataset in case of data loss. Data backup also becomes critical when the data is not needed in a day to day job but can be referred to as a source of truth and for compliance reasons in future. Different types of backup are :

#### Incremental backup
Incremental backup is the backup of data since the last backup, this reduces data redundancy and storage efficiency.

#### Differential backup
Sometimes our data keeps on modifying/updating. In that case we take backup of changes that occurred since the last backup called differential backup.

#### Network backup
Network backup refers to sending out data over the network from the source to a backup destination in a client-server model. This backup destination can be centralized or decentralized. Decentralized backups are useful for disaster recovery scenarios.

**rsync** is one of the linux command which sync up file from one server to the destination server over the network.

#### Cloud Backup
Two most widely used cloud backup options are Azure backup (from Microsoft) and Amazon Glacier backup (from AWS).

## **_Intro to VIM_
Vim is an open-source and free command line editor.
As an SRE we several times 
- log into into the servers
- make changes to the config file 
- edit and modify scripts 

**Opening a file and using insert mode**
We use the command vim filename to open a file filename. The terminal will open an editor but once you start writing, it won’t work. It’s because we are not in "INSERT" mode in vim.

Press i and get into insert mode and start writing.
**Vim Commands	Description**
:q	 Exit the file but won’t exit if file has unsaved changes
:wq	Write(save) and exit the file.
:q!	Exit without saving the changes.

## **_Bash Scripting_
Writing the first bash script:

We will start with a simple program, we will use Vim as the editor during the whole journey.

```sh
#!/bin/bash

# This if my first bash script
# Line starting with # is commented

echo "Hello world!"
```
We will save this script as “firstscript.sh” and make the script executable using chmod.

![alt text](https://linkedin.github.io/school-of-sre/level102/linux_intermediate/images/image16.png)
## 2.Linux Advance
## **_Containers_
A container is your code bundled along with its entire runtime environment. That includes your system libraries, binaries and config files needed for your application to run.

**Difference between virtual machines and containers**

- Containers do not have a separate (guest) OS
- Container engine is the intermediary between containers and Host OS. It is used to facilitate the life-cycle of a container on the Host OS (it is not a necessity, however).

#### VM
![alt text](https://linkedin.github.io/school-of-sre/level102/containerization_and_orchestration/images/VM.png)

#### Container
![alt text](https://linkedin.github.io/school-of-sre/level102/containerization_and_orchestration/images/Containers.png)

**Hypervisor vs. Container Runtime**:

**VMs**: Hypervisors (such as VMware, Hyper-V, or KVM) manage the creation, operation, and monitoring of virtual machines. Hypervisors provide a layer of abstraction between the physical hardware and the VMs.
**Containers**: Container runtimes (e.g., Docker, containerd) are responsible for managing the life cycle of containers. They interact with the host OS and leverage containerization features provided by the Linux kernel (namespaces, cgroups) to create isolated environments.

**Docker Image**
A Docker image is a lightweight, standalone, and **executable package** that includes everything needed to run a piece of software, including the code, runtime, libraries, and system tools. It is a snapshot of a filesystem with the necessary components to run an application.

## **_Orchestration With Kubernetes_
The Kubernetes components themselves are run as containers wrapped in Pods (which is the most basic kubernetes resource object).

**Control plane components**:
- ube-apiserver
- etcd
- kube-scheduler
- kube-controller-manager
- Node plane components
- kubelet
- kube-proxy

This **workflow** might help you understand the working on components better:

1. An SRE installs kubectl in their local machine. This is the client which interacts with the Kubernetes control plane (and hence the cluster).

2. They create a YAML file, called manifest which specifies the desired state of the resource (e.g a deployment names “frontend” needs 3 pods to always be running)

3. When they issue a command to create objects based in the YAML file, the kubectl CLI tool sends a rest API request to the kube-apiserver.

4. If the manifest is valid, it is stored as key value pairs in the etcd server on the control plane.

5. kube-scheduler chooses which nodes to put the containers on (basically schedules them)

6. There are controller processes (managed by kube-controller manager) which makes sure the current state of the cluster is equivalent to the desired state (here, 3 pods are indeed running in the cluster -> all is fine).

7. On the node plane side, kubelet makes sure that pods are locally kept in running state.

## 3.Database Design

1. ERD Diagram design from a crud expense apllication scenario
2. Later Relational Database Design from this
3. Implement query 
4. Finally, Implement the whole application

**github URL**: https://github.com/galib-1206/Expense_Tracker

## 4. CI/CD Pipeline
**Continuous Integration**:
Continuous Integration is a practice followed by the developers. Which includes time-to-time check-ins to a shared repository.
Stages of CI :
 1.Push
2.Test
3.Fix
**Continuous Delivery** :
Continuous delivery (CD) picks up where continuous integration is over. While CI is the process to build and test automatically. CD deploys all code changes to the testing or staging environment in the build.

![alt text](https://miro.medium.com/v2/resize:fit:720/format:webp/1*S8zzQ_113f6xFxqXATS4ng.png)

**Tools Of CI/CD** :
![alt text](https://miro.medium.com/v2/resize:fit:1100/format:webp/1*QNyCzVKmGFBm9LshdAEYOQ.png )

**Jenkins** is a powerful Java-based tool and is widely used. It is mostly known for its flexibility. **It is an open-source automation server is written in Java**. It also supports version control tools like Subversion, Git, Mercurial, and Maven. It is well-documented & extremely extensible, with a rich ecosystem of plugins and integrations.

**GitLab** is a web-based Git repository manager. It has a wiki, issue tracking, and CI/CD pipeline features, using an open-source license.

**CircleCI** is a lightweight **cloud-based** CI/CD platform. It automates build, test, and deployment processes. It has a readable YAML configuration, is painless to set up, and does not need a dedicated server to run. It is suitable for small projects that need to get off the ground fast.

**Codeship** by CloudBees is a hosted Continuous Delivery platform. It helps to release software quickly, automatically, and many times a day. It integrates with GitHub and BitBucket. **Automatically deploying when tests pass.** Notifying you when tests or deployments have failed.

GoCD is an open-source software development tool that automates the CD of software. It has value stream mapping, cloud-native deployments, complex workflow modeling, and advanced traceability.

Apart from these widely used tools, there are a few more tools available in the market. Like Azure, Spinnaker, Travis CI, Buddy, Bamboo, and many more. You can choose any of them as per your need and suitability.

### Github Action 
Suppose i have a main branch and an FastApi application is running on it. 
Now i will have to create a new branch named 'dev' . my main branch is protected type. 
After i will create a remote branch named  'galib' , there i will do some change in the code. 
After that i will do the git commands form galib branch like (git add . , git commit , git push origin galib) . If i do this , then a pull request is created from branch galib to branch dev.
Then comes the concept of pipeline.  Here pull request is called a event.  so, for this pull request pipeline(event1).
 - **Pull request ->Unit testing -> Review (manual or automatic)->Merge Approval** .

## AWS
### EC2
### Parameter storing 
### Enviorenment variables set up.
link: https://www.youtube.com/watch?v=dbHaCX14nKw

### ECS
CAAS: Container as a service. 
Whole infrasructure is not needed. so, it's less costly.
Basically, Application -> Docker Container -> Docker image pushing to ECR -> Run ECS

Under ECS, there will be **Task** managed by service.
Task contains env variables, config files.
Task knows how to run a image. 
service runs the task under ECS cluster.Also can scales up and down the tasks.
link: https://www.youtube.com/watch?v=AiiFbsAlLaI
### CodePipeline

### ECR 
ECR is likely to Docker Hub.
After SSH to an EC2 instance from remote server, if this command is run :
```sh 
./reboot_backend.sh 
```

- The script stopped and removed several Docker containers (dev-app, redis-dev-server, dev-db).
- It then removed the Docker network task-station-dev_default.
- After that, it logged in to your Docker registry (AWS ECR) successfully.
- Next, it pulled the latest image (task-station23-dev:latest) from the AWS ECR repository.
- Finally, it recreated the Docker containers (dev-db, redis-dev-server, dev-app) using the pulled image.
Your backend services should now be rebooted and running with the latest changes. 

### CloudFront

### Lamda
**Serverless Computing** : 
Lambda is a serverless platform, meaning you don't need to worry about provisioning, scaling, or managing servers to run your code. You simply upload your code, and Lambda handles the rest.
- A function is defined 
- when an event is occurred , lamda basically triggered the function and handles the rest.
- It takes 2 parameters : handler Function (event, context)
- it also accepts libraries for API call and show output

**Layer** :
it basically contains library & packages.
As Lamda is serverless and can't install library. So, layer is needed.

**API Gateway Integrate**
- api is created in AWS API Gateway
- then it is triggered with Lamda function
- so Using URL, response canbe retrieved from any screen or browser. No server is needed.

secure: SSL
packet lock kora. CloudFront e auto secure hoye jai.
hacker can't capture packet by third party soft like wireshark.

**Nginx as a loadbalancer**
3 types:
1. Simple load balancing : Round Robin (simply numbering)
2. Weighted approach : depends on ram power
3. Least Connection : Req will be sent to the server which has less connections.
link: https://www.youtube.com/watch?v=nmRvFRvkubc

#### **Proxy vs Reverse Proxy** : https://www.youtube.com/watch?v=nmRvFRvkubc

**Proxy:** Client ar internet er middle e bose. 
Mainly , client er hoye kaaj korbe. 
- protects client online identity
- bypasses browsing restrictions
- blocks access to certain content

**Reverse Proxy:** Client er req receive kore, website e distribute korbe. Mainly website er hoye kaaj korbe.
- protects website ip from clients
- load balancing 
- caching static content 
- handles SSL encryption

## Taskstation-stage-backend
so, basically ..
- codepipeline run korle , docker image create hobe which contains the whole application.
- docker-compose.yaml file e backend service, mongo, redis define kora. 
- virtual server (EC2) te docker-compose up korle , auto install hobe.
- mondoDB data dekhte hoile MongoCompass install korbo.
- yaml file dekhe dekhe , security group & Build er Enviorenment variables set korbo. (url, port, hostname)
- build pipeline er logs theke issue ber kore troubleshooting korbo
- ultimately, backend server up & running kina check korbo! 
```sh 
sudo docker-compose logs -f
```
- Ping:Pong asle all Okay.

**Trouble shooting:**
1. too many requests, docker imaged failed to pulled.
-> each time pipeline chalaile docker image create hobe. ekta limit ase. limit cross korle ar pull hobe na.
so, sourcecode e ECR theke direct pulling er directory define kore dibo.
2. pipeline er build e enviorenment variable e basically docker-container er port assign kora lagbe. As, (mongoDB, Redis) now , host theke Container e exist kortese.
Eg, Host port : Container Port = 29017:27017

some useful commands for checking : 
```sh

ip addr 

sudo docker network ls

sudo docker network inspect <id>
```
###ECS: 
**  Why ECS is needed? 
1. docker is for one server , ECS accepts multiple server 
2. Better & simple GUI for  loadbalancing , scaling up and down. 

ECS has 2 launch types 
1.EC2 
2.Fargate (serverless)

ECS doesnot have any server , it has clusters.
**ECS Launch:**
- ECS having clusters
- Clusters are basically physical resources , where container will be run on.
- inside cluster, we have to setup infrastructure of EC2 server manually.
- Inside EC2 , ther will be 
    ->docker
    ->ECS Agent
    ->firewall
    ->patches
so, overall..
1.We need to manage EC2 manually
2.But, ECS manages the containers.
3.In this way , Full control over infrastructure.

**Fargate Launch**
- Serverless Archi.
- Inside clusters, there is no server.
- Fargate will create server like EC2 on demand.
- No need to maintain servers. Fargate will do it
- Less costly.

**ECS Task :**
- A blueprint which defined a running container. Basically like a docker image.

**ECS sevices**
- Ensures tasks are running or not 
- Restart containers , if fails
- distribute EC2 instance 

**Service Updated**
Each time ip will be changed!!!
Each task has individual ip.

**Task Definition**
**-> Add Volume in Container**
Container gulor EFS(Elastic File Syestem) config korte hobe! 
Security grup create korte hobe , appropraite vpc niye.

**-> Add Mount points in Container**
Container path, Eg: /data/db

**Service**
**-> Load Balancer**
- Application load balancer(ALB). 
- security grup create
- Port 80 dibo. As, Traffic port 80-> 3000 e redirect hobe.
- Health check defined.

# CTMS-system

**IUT CSE FEST-2024** Hackathon DevOps Segment Team team_naam_nai

Basically, We developed **Car Trading Management System** that includes a range of functionalities such as -
1. Registered Users can apply for Car Trading.
2. Adding and viewing Car post in User Dashboard.
3. Multiple Payment option, Price wise sorting.
4. Using Cloudfront and Amazon S3 for frontend deployment and Amazon CodePipeline and CodeDeploy for backend deployment.
5. Using Route53 for assigning custom DNS, SSL Certificate taken from Certificate Management.
6. Amazon Cloud watch for monitoring, Terraform for infrastructure automation, Application Load Balancer (ELB).
7. Mailing Service (SNS) during Autoscaling and EBS Snapshots Lifecycle for Backup.

# Stage 1

A UI app where users can login and register account. Implement automated testing and deployment pipeline

# Stage 2

Add and View Car post in User dashboard.

# Stage 3

View all the car posts in Home. Automated infrastructure scaling is implemented.

## Here is our solutions:

### Stage 1: Progress

Frontend:A simple frontend UI created with react
Testing: Introduced Unit testing and integration testing with supertest and jest.
Backend: A backend app created with express.js
CI/CD: Frontend CI/CD pipeline created using AWS codePipeline
Git branching: best practices were used to maintain branching
strategy for seamless collaboration and automates testing.

# Git Branching Strategy

Main: Main production branch

Develop: Development branch

QA: Branch for quality assurance test

Stage: Final requirements check before merging to main

Feature: Feature branch for developing multiple features simultaneously

### Stage 2: progress

Infrastructure automation: Introduced infrastructure
automation for more flexibility during deployment

### Stage 3: progress

Implement : UI was updated to show car posts in home.
Infrastructure scaling: Infrastructure was configured to scale automatically during heavy load

## Auto-Scaling Policy

# ScaleUp Policy

CloudWatch Metric :

CpuUtilization

    Rule :

      Average CpuUtilization = 30

    Add Instance = 1

# Final Architure of the system
![alt text](https://github.com/rakib3004/VMS-backend/blob/main/Architecture.png?raw=true)


These are the links for individual repositories

CTD_Frontend: https://github.com/SwarnaIslam/Frontend_DevOps/tree/frontend

CTD_Backend: https://github.com/SwarnaIslam/Backend_DevOps

CTD_Slide: https://docs.google.com/presentation/d/1aKeX0ZUB2nPybSfRaSQCk8AjWAOzebVe6nm27Kx_P1g/edit?usp=sharing

forntend link: https://ctd.projectsbd.me

# Kubernetes

Kubernetes Principle : 
Desired State : Configuration.
Controllers : changed states.
API server : defined objects with states. Central communication hub.

**Kubernetes API : 
pods : singel or multtiple containers  
probes : health check of pods.

controllers : controlling pods up and running .
- defined your desired state.
- create and manage pods
- ReplicaSet controller
- Deployment - ReplicaSet manage kore.


services: 
Adds persistency to our ephemeral world.
- Networking config for pod access
- Ip and DNS name for the service.
- Dynamically update routing information on Pod lifecycle .
- so that if users access the persistant ip , kubernatese routes the traffic directly
to pods.

Storage : 
Persistent Volume : pod independent volume ( decoupled storage from cluster)

Cluster Components 

Control Panel node : 
- Master node 
- Cluster operations 
- monitoring 
- pods scheduling 
- access point of cluster administration 
Consists of 
- API server : primary access point for cluster and administrative operations (Communication hub)
- etcd : store the states of api server 
- scheduler : tells nodes to which pods will be start off
- controller manager : keeping things in the desire state and mIntaining lifecycle.
- Kubectl : administrative cli command to interact with api 
Node :
- Worker node where our application pods are running 


Installation : 
Cloud 
On premises

Building your cluster : 
- install and config packages 
- create cluster 
- config pod networking 
- join m=nodes to cluster 

Required packages : 
- containerd : docker 
- kubelet : drive the work in individual nodes 
- kubeadm : up and running the cluster components
- kubectl : administrative cli command 

Install kubernetes on VMs


# ShopSwift (Final Devops Project)

This repository contains a Django and React ecommerce project. 
Among other functionality, 
- users can create their account, 
- add items to their cart and 
- purchase those items using Stripe.


## Backend development workflow

```json
python version recommended 3.8.10 
virtualenv env
source env/bin/activate
pip install -r requirements.txt
python manage.py makemigrations
python manage.py migrate
python manage.py runserver
```

## Frontend development workflow

```json
nvm version recommended 16
npm i
npm start
```

## For deploying

```json
npm run build
```

# MInikube Cluster : 
###  VM Setup

1. Setup Virtual machine in Virtual Box
If virtual support manager not enabled , then run these commands on local machine ( vm must be stopped then) : 
 
 ```json
 Vboxmanage modifyvm “vm_name”  --nested-hw-virt=on
 ```

2. Now install  Minicube for Kubernetes Cluster. 

### Minikube.sh : 
```json
#!/bin/bash

sudo apt-get update -y
sudo apt-get install curl wget apt-transport-https virtualbox virtualbox-ext-pack -y
echo "1st install docker"
sudo apt update && apt -y install docker.io
sudo systemctl start docker
sudo systemctl enable docker
sudo chmod 666 /var/run/docker.sock

echo "Apply updates"
sudo apt update -y
sudo apt upgrade -y

echo " Download Minikube Binary"
wget https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo cp minikube-linux-amd64 /usr/local/bin/minikube
sudo chmod +x /usr/local/bin/minikube
minikube version


echo "Install Kubectl utility"
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
kubectl version -o yaml

echo "Start the minikube"
minikube start
minikube status
```


Open terminal to this location and run : 
            
    Sudo chmod +x minikube.sh
          
    ./minikube.sh


Start Cluster :
 ```json
 minicube start
 ```
### Deploy a demo application 

**Deploy application (service):**

Create a sample deployment and expose it on port 8080:
```json 
kubectl create deployment hello-minikube --image=kicbase/echo-server:1.0
kubectl expose deployment hello-minikube --type=NodePort --port=8080
```
It may take a moment, but your deployment will soon show up when you run:
```json
kubectl get services hello-minikube
```
 The easiest way to access this service is to let minikube launch a web browser for you:
```json
minikube service hello-minikube
```
Alternatively, use **kubectl** to forward the port:
```json
kubectl port-forward service/hello-minikube 7080:8080
```
Tada! Your application is now available at http://localhost:7080/.

Source : 
https://minikube.sigs.k8s.io/docs/

#### Deployment of Fastapi-Application
**Docker Container:** 
<Fastapi-hello-world files >
**_Dockerfile  |  main.py  |  requirements.txt_**

 Build the docker image :
```json
docker build -t galib9940/fastapi-hello-world .
```
Docker Image Name: galib9940/fastapi-hello-world
Docker Hub Username: galib9940
Repository Name: fastapi-hello-world
Tag: latest (default)

Check images : 
```json
docker images
```
Run the docker Container : 
```json
docker run -d -p 8000:80 --name fastapi-container galib9940/fastapi-hello-world
```
Run a container from your existing Docker image. This will map port 8000 on your host to port 80 in the container.
Check the container : 
```json
docker ps 
docker logs fastapi-container
```
Access the FastAPI application:  curl http://localhost:8000


**Docker Compose** : 
For multiple container application 
Need a docker-compose.yaml file


**Deployment Hierarchy:** 
#### _Ingressing <- Service <- Deployments <- Replica Set <- Pods_

- Pods >> container , because multiple pods can be running at the same time.

- Service is served like a proxy for multiple pods ip. 
If client hit on the service port , then service forwards to the appropriate port.

- memorizing ip address is difficult , so hitting the application with a domain name. 
That’s why ingressing concept is needed!  

**Ingressing**
Ingress exposes HTTP and HTTPS routes from outside the cluster to services within the cluster.

![alt text](https://earthly.dev/blog/assets/images/mutual-tls-kubernetes-nginx-ingress-controller/ptpr1xB.png )

Enabling ingress 
```json
Minikube addons enable ingress 
```
Yaml file creating (services,pods,ingress) 
```json
Kubectl apply -f <file.yaml>
```
If namespace is created , then… ( isolate resources : deployment, services, ingress)
```json
Kubectl get pods -n <namespace_name>
Kubectl get service -n <namespace_name>
Kubectl get ingress -n <namespace_name>
```
**Domain Resolution** 
Ensuring domain name (galib123.com) points to the correct ip address of your ingress controller or minikube cluster 

1. Verify ip:( ip will be same for minikube cluster and ingress controller )
```json
minikube ip  
Kubectl get ingress -n <namespace> o -wide
```
 
2. DNS configuration : nslookup galib123.com (should display the ip address with your domain)

If failed , then -> 
Make sure that , Minikube ip or ingress controller ip is reachable from your host machine!! 

To check : ping ip_address ( sends ICMP echo req and wait for response)
3. Check ingress controller(nginx) is running properly or not. 
```json
kubectl get pods -n kube-system -l app.kubernetes.io/name=ingress-nginx
```
This command filters the pods in the kube-system. If not found , then create a one . 
4. To check all from ingress-nginx:
```json
kubectl get all -n ingress-nginx
```
**To check for all the endpoints and ingress :** 
```
Kubectl get ingress -A
Kubectl get endpoints -A
Check logs : controller is getting req or not .
kubectl logs -f <nginx-ingress-controller pod id>   -n ingress-nginx
```
#### Nginx-Ingress-Controller
**Still getting error while hitting  at the domain galib123.com** ??
So the mechanism is basically , when i hit at domain , it forwards to ingress controller external ip ( which is basically virtual machine’s host only adapter ip :  192.168.56.101  & this is the ip should be  config in local host (/etc/hosts) 
Cli command : 
```json
cat /etc/hosts
127.0.0.1	localhost
127.0.1.1	bs949
192.168.56.101    galib123.com (defined)
```
But unfortunately , we can’t deine external ip into the minikube cluster Nginx controller service. So a routing table should be created , so that ,
**_Domain hit -> External ip -> Routing table -> ingress controller ip -> application_**
But this is not a good practice. So, you can use Load Balancer as a service. 
otherwise, use kubeadm cluster instead of minikube.
link: https://docs.google.com/document/d/1Q770dZRTpCCU8lMtP1kYFogKq8sUH6Q15IaNDttCFqI/edit?pli=1

# Deploy application with Kubeadm Cluster  

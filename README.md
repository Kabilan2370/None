### 1. What is Docker Swarm ? Why we are using this ?
Docker Swarm is a native container orchestration tool built into the Docker Engine that allows you to manage a cluster of Docker hosts as a single virtual system. 
It is designed for simplicity and ease of use, allowing users to deploy, scale, and manage applications across multiple machines using familiar Docker CLI commands. 

We use Docker Swarm to transition from running individual containers on a single host to running robust, scalable, and highly available services in a clustered environment. 

Prerequisites, if we want to setup docker swarm
1. Linux VM / EC2 / Local machine

2. Docker installed

3. Ports open (2377, 7946, 4789)

Once setup the prerequesites init the docker swarm then a join token will be shown

    sudo docker swarm init --advertise-addr 172.30.118.228

Eg: docker swarm join --token SWMTKN-1-0mhdweqogeu960mwdkhzjae1w7cjnhxn5y2w139h38ozaz70rv-eoaqlnnb7wprevlug0xwbqhty 172.30.118.228:2377
sudo docker swarm leave --force


### 2. How the worker node can join into docker swarm masternode ?
The master note should that token to invite the worker nodes

    sudo docker swarm join --token <> <master-ip>:2377

to verify the worker node has joined or not

    sudo docker node ls

### 3. we can check the running and stopped container list using "docker ps -a" command
To check the docker swarm container we can check using docker service command

    sudo docker service create \
    --name app1 \
    --replicas 3 \
    -p 80:80 \
    nginx:latest

We can check and list out the swarm service containers

    sudo docker service ls
    sudo docker service ps app1

### 4. We can scale the service, using 

    sudo docker service scale app1=5


### 5. What is Cron ?
Cron is a time-based job scheduler in Unix-like operating systems (Linux, macOS) that automates repetitive tasks by running commands or scripts at specified intervals, 
like daily backups, email reminders, or system cleanups, saving manual effort and ensuring timely maintenance without user intervention. 


### 6. In Docker Swarm, you can implement cron jobs using a few different approaches :
In Docker Swarm, you can implement cron jobs using a few different approaches, as Swarm mode itself does not have a built-in "CronJob" object like Kubernetes. The most common methods involve.

###  Running Cron Inside a Container
This traditional approach involves packaging the cron daemon and your scripts within a single Docker image and keeping the container alive by running cron in the foreground. 

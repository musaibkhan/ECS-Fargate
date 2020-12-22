---
title:  ECS Setup using Fargate
weight: 5
---
***
## Aim

The aim of this document is to help you to Setup ECS Fargate cluster, and deploy a web application using it.

![ecs-fg-23.png](/images/ecs-fg-23.png)

## Solution Approach
The approach for the Solution would be:

1. Creating ECS Fargate Cluster
2. Create a task definition for our application.
3. Create a service for running a task(app).

## Prerequisites

In order to get started, you’ll need to have completed the following steps.

* Have an AWS Account.(with enough permission to create and destroy ECS resources)
* Set your AWS Region to one where ECS Fargate is available.

##  Setting up ECS from the AWS Management Console


### Step-1:  Configure a Cluster
1. Open the Amazon ECS console at https://console.aws.amazon.com/ecs/
2. From the navigation bar, select the Region to use.
3. In the navigation pane, choose Clusters.
   
![ecs-fg-1.png](/images/ecs-fg-1.png)

4. When creating a new Cluster you will get the choice of launch compatibility. Choose "Networking Only" and click next.
   
![ecs-fg-3.png](/images/ecs-fg-3.png)

5. you enter the name you want your cluster to have. I named mine “MyClusterName”. (Optional-you also can craete a Virtual Private Cloud (VPC) which will give you access to a range of local ip-addresses and subnets.)
   
![ecs-fg-4.png](/images/ecs-fg-4.png)

6. Click “Create” and wait while AWS generates your cluster. When it’s done go back to the ECS-console to view your cluster.
   
![ecs-fg-5.png](/images/ecs-fg-5.png)
   
 ### Step-2:  Create a Task Definition

The next thing we need to do is to create a task-definition. 

1. click on Create new Task Definition under Task Definition.

![ecs-fg-7.png](/images/ecs-fg-7.png)

2. When creating a new Task Definition you will get the choice of launch compatibility. Choose Fargate and click next.

![ecs-fg-8.png](/images/ecs-fg-8.png)

3. Name your task and select a task role. I just select the default IAM role ecsTaskExecutionRole.

![ecs-fg-9.png](/images/ecs-fg-9.png)

4. Set your preferred task memory and task cpu. I don’t need much for my simple image to run so I just choose the lowest possible options.

![ecs-fg-12.png](/images/ecs-fg-12.png)

5. Scroll down and find the add container option. Here you enter a name for the container and the Image name (If you are using Image from ECR and you don’t remember it, open a new tab and go to ECR to get find it.)

![ecs-fg-11.png](/images/ecs-fg-11.png)

6. Set the port to the same port that your docker container exposes. You can define a lot more options for your container, but you don’t need anything more for it to run. So right now we won’t bother.


Press “Create” and you are all set to create a service to run the Task Definition

### Step-4: Create a service

This is the most involved process so far, we need to configure our service and a security group for our cluster.

1. Lets go back to the ECS-console and enter your Cluster. Click “Create” under the Services tab.

![ecs-fg-13.png](/images/ecs-fg-13.png)


2. Once again you will be given the choice of Fargate vs EC2. And once again you will select Fargate). You will also see that your Task Definition is preselected with the latest revision(if you for some reason made more than one). Name your service and select how many tasks you want to run. If you enter «2» it will start two instances of your container.

![ecs-fg-14.png](/images/ecs-fg-14.png)

![ecs-fg-15.png](/images//ecs-fg-15.png)

3. In the next step we need to choose a VPC (Virtual Private Cloud) and subnets which we already have generated. Select the subnets available.

![ecs-fg-17.png](/images/ecs-fg-17.png)

![ecs-fg-18.png](/images/ecs-fg-18.png)

4. Let's quickly review the service, if everythings Ok, click "create service".

![ecs-fg-19.png](/images/ecs-fg-19.png)

4. Next up is the security group for the cluster. Click “Edit” and and set a custom TCP-port if your container uses anything other than port 80. For now we will keep it open from anywhere and go back to adjust the source “My-service-Name” to easily see that it belongs to my cluster.
5. let’s test if we can access the app. Do this by clicking on the task name and find its Public IP address. Enter the IP-address in the browser and append the port of the container like this:- http://0.0.0.0:80

![ecs-fg-20.png](/images/ecs-fg-20.png)

![ecs-fg-21.png](/images/ecs-fg-21.png)

If it’s accessible, congrats.

## FAQ

#### Q: What is Amazon Elastic Container Service?

Amazon Elastic Container Service (ECS) is a highly scalable, high performance container management service that supports Docker containers and allows you to easily run applications on a managed cluster of Amazon EC2 instances.You can use Amazon ECS to schedule the placement of containers across your cluster based on your resource needs and availability requirements. 

#### Q: Why should I use Amazon ECS?

Amazon ECS makes it easy to use containers by eliminating the need for you to install, operate, and scale your own cluster management infrastructure. Amazon ECS lets you schedule long-running applications, services, and batch processes using Docker containers. Amazon ECS maintains application availability and allows you to scale your containers up or down to meet your application's capacity requirements. Amazon ECS is integrated with familiar features like Elastic Load Balancing, EBS volumes, VPC, and IAM. Simple APIs 

#### Q: What is AWS Fargate?

AWS Fargate is a serverless compute engine for containers that works with  Amazon Elastic Container Service (ECS). Fargate makes it easy for you to focus on building your applications. Fargate removes the need to provision and manage servers, lets you specify and pay for resources per application, and improves security through application isolation by design.

#### Q: Does ECS Fargate invlolve costing?

With AWS Fargate, there are no upfront payments and you only pay for the resources that you use. You pay for the amount of vCPU and memory resources consumed by your containerized applications.&nbsp;&nbsp;[Click Here for ECS Fargate Pricing](https://aws.amazon.com/fargate/pricing/)
<br />

## Author of the Document

#### Name: Musaib Khan

#### Email ID: musaib.khan@tothenew.com

#### Mob No.: +91-9911595503

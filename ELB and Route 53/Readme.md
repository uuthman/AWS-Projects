# Deploying a multiple compute resources on the cloud, when the load increases and the cpu utilization exceeds 80% and then remove the resources when the cpu utilization goes under 60%
# We create a load balancer to distribute the load between compute resources and route the traffic to a domain

#### Here is an architecture diagram
![Architectural Diagram](images%20/diagram.png)

The first step is to ensure we have a vpc to use
- We can do this by creating a vpc or using the default vpc in the region we selected
- After creating a vpc, we create an ec2 instance 
- To create an ec2 instance we go to the search bar enter ec2 then click on the ec2 menu shown
  ![EC2 Search](images%20/ec2.png)
- After clicking, it navigates us to the ec2 page 
- Then click on launch an instance 
- It navigates to the Launch an instance page
- First thing is to give the instance a Name
- Select the AMI we want to use (I will be using Ubuntu)
- Then we select an Instance type (I will be using t2.micro)
- The next thing is to generate a key pair 
- Then we move to the network settings
- First thing to do is to select a VPC
- Then select a subnet 
- Add a security Group
- I will use the default storage 
- Then click on launch instance to create an ec2 instance 

To make use of auto scaling group we need to create a Launch Template and to create a launch template we need can either use the AMI provided on aws or we create our own AMI

We are going to create our own ami because we need to set up a webserver on it and also show a static website 

We will make use of the ec2 instance we created 

First thing to do is to set up our webserver and add a static website 
- We can do this by connecting to the cli and install apache2 on it
- Then create an index file and add your html body to it
- The next step is to move the index file to /var/www/html/
- We then start our server 

After confirming that everything is fine, the next step is to create our own AMI from the ec2 instance



# Deploying a multiple compute resources on the cloud, when the load increases and the cpu utilization exceeds 80% and then remove the resources when the cpu utilization goes under 60%
# We create a load balancer to distribute the load between compute resources and route the traffic to a domain

#### Here is an architecture diagram
![Architectural Diagram](images%20/diagram.png)

The first step is to ensure we have a vpc to use
- We can do this by creating a vpc or using the default vpc in the region we selected
- After creating a vpc, we create an ec2 instance
- To create an ec2 instance, we go to the search bar, enter EC2, then click on the ec2 menu shown
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

To make use of auto-scaling groups, we need to create a Launch template. To create a launch template, we can either use the AMI provided on aws or create our own AMI

We are going to create our own ami because we need to set up a webserver on it and also show a static website

We will make use of the ec2 instance we created

First thing to do is to set up our webserver and add a static website
- We can do this by connecting to the cli and install apache2 on it
- Then create an index file and add your html body to it
- The next step is to move the index file to /var/www/html/
- We then start our server

After confirming that everything is fine, the next step is to create our own AMI from the ec2 instance
- Navigate to the instance page
- Select on the instance created
- Click on the action button
- Click on Image and templates from the menu
- Select Create image from the submenu.
  ![Create Ami](images%20/create-ami.png)

To confirm the created AMI, on the side menu by the left, click on AMI from the images section, and then we see our created AMI
![AMI TABLE](images%20/ami-table.png)
The next step is to create a Launch template to be used by the auto-scaling groups
- Click on launch templates from the side menu on the left
- Next thing is to click on Create launch template to navigate to the page to create a launch template
- Enter a launch template name
- Enter the description of the launch template
- Then to the Launch template contents
- Select the ami we created
- Select the instance type
- Select the key pair login
- In the network section, Add a security group
- Click on the Create launch template button to create a template
  ![AMI TABLE](images%20/launch-template-table.png)

The next step is to create a target group for load balancer
- Click on Target Groups from the side menu on the left under the Load balancing section
- Click on the Create target group button to navigate to the page to create a target group
  The first thing is to choose a target that will be instance for us
- Enter a target group name
- Select a protocol: Port, we will be using protocol HTTP and port 80
- IP address type will the IPv4
- Select the vpc
- And the protocol version will be HTTP1
- Leave the health checks the way they are.
- Click on the next button
- Click on the Create target group button to create a target group
  ![TARGET TABLE](images%20/target-group.png)

The next step is to create a load balancer 
- Click on Load balancer from the side menu on the left under the Load balancing section
- Click on the Create load balancer button to navigate to the page to create a load balancer
- Since we are making use of the HTTP protocol, we are going to create an application load balancer
- Click the Create button on the application load balancer
- Enter the load balancer name
- Select a scheme, We are going to make use of the internet facing since we want people to access it from the internet
- select IPv4 for the IP address type
- Select our vpc in the network mapping section
  Select a security group
- Under the listeners and routing section, for protocol and port, it will be HTTP and 80
- Select the target group we created
- Click on the Create load balancer button





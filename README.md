Building a Secure VPC with Private Subnets and NAT

![image](https://github.com/Yogeswari-369/VPC_Demo/assets/85894796/3c3ee24b-2ed1-49af-a1ba-aea63ccb51a4)

This project demonstrates how to create a VPC that can use for servers in a production environment.

---> To improve resiliency, deploy the servers in two Availability Zones, by using an Auto Scaling group and an Application Load Balancer. For additional security, deploy the servers in private subnets. The servers receive requests through the load balancer. The servers can connect to the internet by using a NAT gateway. To improve resiliency, deploy the NAT gateway in both Availability Zones.. Let's dive into the details! 


Project Highlights:

* The VPC has public subnets and private subnets in two availability zones

* Each public subnet contains a NAT gateway and load balancer

* The servers run in the private subnets are launched by using Auto Scaling group and receive traffic from the load balancer

* The servers can connect to the internet by using the NAT gateway


Deep Dive into the Setup:



✴ Creating 2 availability zones because if the data center in one availability zone in a specific region goes down we will still have the other availability zone which is up and running


✴ NAT Gateway: The application inside a private subnet should get some data from APIs or download some packages from outside the internet, then NAT Gateway will mask the private IP with public IP and get the required information from outside the internet.


✴ Auto Scaling Group: It will create a number of instances to scale automatically
    We should deploy application in 2 availability zones instead of creating 2 instances manually we can create auto scaling group and define how many instances we want to launch then auto scaling group automatically create new instances based upon the configurations defined in auto scaling group.
    If application is getting more requests our 2 EC2 instances will handle only 100 requests if we are getting 200 requests then automatically auto scaling will increase the instances based upon the requests coming to our application.


✴ Load Balancer: It will distribute the load between the availability zones based upon the number of requests we are getting
      If we are getting more load it will distribute based upon the number of requests coming. If one instance has more capacity then it will automatically send the 60 requests to one instance and 40 requests to another instance.
      

✴ Bastion Host:
       The instances inside the private subnets don’t have public IP address so we can’t do ssh to these instances inside private subnet directly. 
       Created a Bastion host inside public subnet and through the bastion host connected to the instances inside private subnets.


![image](https://github.com/Yogeswari-369/VPC_Demo/assets/85894796/58d37082-1e4e-4c53-8f0a-e473a598992a)



![image](https://github.com/Yogeswari-369/VPC_Demo/assets/85894796/e81af17b-24db-4373-8e2c-88dde36b4d5c)




# AWS-Cloud-Configuration-Application Load Balancer-Fargate
Configuration of AWS Fargate service, Application Load Balancer, and Route53

Target Group Configuration

We need to define target group for Load Balancer to find out where to route the requests.
![lab-node-rds-api-target-group](https://user-images.githubusercontent.com/6191308/162834775-67fb0929-06dd-4452-ab0d-4c95b51769b8.png)

It is importatant to have health check properly define otherwise target group will keep deregistering service attached. This will cost you computational cost as well as unable to keep the connection to api.
First needed item is healthckeck endpoint must be implemented in the code.
![healthcheck-implementation](https://user-images.githubusercontent.com/6191308/162836653-6b4a433e-d281-41c2-9c60-d249cce9800c.png)

Second, healthcheck endpoint must define in Target Group
![target-group-healthcheck](https://user-images.githubusercontent.com/6191308/162836752-b09aeb75-40b1-4b40-8867-654d7c44beb2.png)

Here are created list of Target Groups.
![Target-groups](https://user-images.githubusercontent.com/6191308/162837162-71a2b9f8-ba50-4062-8d63-de05e523b101.png)

In addition, Target group attributes - Deregistration delay, I placed to maximum.


Aplication Load Balancer
Now Load Balancer can create attaching defined Target Groups. When attaching I used my container port 3040, where Load Balancer route requests to container port. After creating Load Balancer, I have defined my routes to different ports. Since I used type IP Applcation Load Balancer, I cannot use Path for routing.
![load-balancer-route-configuration](https://user-images.githubusercontent.com/6191308/162837897-954c6fdf-1e8f-4651-b0e0-083a22d565fd.png)


Application Load Balancer Security Group
Load Balancer's security group needed to refer in each of Security Groups of Services defined in the ECS Cluster. 
![Lab-ALB-Security-Group](https://user-images.githubusercontent.com/6191308/162560846-b0510e36-3e89-49f9-8058-7aa62ac34d32.png)

How to create Cluster, Service and Security Group Confguration described in 
[AWS-Fargate-Configuration](https://github.com/cssamLabs/AWS-Fargate-Configuration/edit/main/README.md)


Load Balancer configuration with Route53
First create Hosted Zone. Then added A Record value as the Load Balancer.
![hosted-zone-alb-config](https://user-images.githubusercontent.com/6191308/162838943-f903e5bc-0269-457d-a0d1-b4cf033ddf07.png)




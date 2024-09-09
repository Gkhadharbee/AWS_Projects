# VPC with servers in private subnets and NAT Gateway
About the project
	This example demonstrates how to create a VPC that you can use for servers in a production environment.
To improve resiliency, you deploy the servers in two availability zones, by using an Auto Scaling group and an Application Load Balancer. For additional security, you deploy the servers in private subnets. The servers receive requests through the load balancer. The servers can connect to the internet by using a NAT gateway in both Availability Zones.

<img width="305" alt="image" src="https://github.com/user-attachments/assets/be9421fd-745e-4bd4-a36f-664a00ca28a8">


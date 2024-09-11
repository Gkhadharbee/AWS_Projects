
# <p align="">VPC with servers in private subnets and NAT Gateway
## <p align="">About the project</p>
  This project demonstrates how to create a VPC that you can use for servers in a production environment.
To improve resiliency, you deploy the servers in two availability zones, by using an Auto Scaling group and an Application Load Balancer. For additional security, you deploy the servers in private subnets. The servers receive requests through the load balancer. The servers can connect to the internet by using a NAT gateway in both Availability Zones.

![](https://docs.aws.amazon.com/images/vpc/latest/userguide/images/vpc-example-private-subnets.png)

## Overview

The VPC has pulic subnets and private subnets in two Availability Zones.
Each public subnet contains a NAT gateway and a load balancer node.
The servers run in the private subnets, are launched and terminated by using an Auto scaling group, and receive traffic from the load balancer.
The servers can connect to the internet by using the NAT gateway.

## Pre-requisites

•	Auto scaling group  
•	Load balancer  
•	Launch Template  
•	Target group  
•	Bastion host or Jump server  

## <p align="">Steps</p>
  

### <p align="">Step1:</p>
  
Create the VPC :  
a.	Open the Amazon VPC console at https://console.aws.amazon.com/vpc/.  
b.	On the dashboard, choose Create VPC.  
c.	For Resources to create, choose VPC and more.  
d.	Configure the VPC:  
  a.	For Name tag auto-generation, enter a name for the VPC.
  b.	For IPv4 CIDR block, you can keep the default suggestion, or alternatively you can enter the CIDR block required by your application or network.
  c.	If your application communicates by using IPv6 addresses, choose IPv6 CIDR block, Amazon-provided IPv6 CIDR block.
e.	Configure the subnets
  a.	For Number of Availability Zones, choose 2, so that you can launch instances in multiple Availability Zones to improve resiliency.
  b.	For Number of public subnets, choose 2.
  c.	For Number of private subnets, choose 2.
  d.	You can keep the default CIDR block for the public subnet, or alternatively you can expand Customize subnet CIDR blocks and enter a CIDR block. For more information,        see Subnet CIDR blocks.
f.	For NAT gateways, choose 1 per AZ to improve resiliency.
g.	If your application communicates by using IPv6 addresses, for Egress only internet gateway, choose Yes.
h.	For VPC endpoints, if your instances must access an S3 bucket, keep the S3 Gateway default. Otherwise, instances in your private subnet can't access Amazon S3. There is no cost for this option, so you can keep the default if you might use an S3 bucket in the future. If you choose None, you can always add a gateway VPC endpoint later on. So, Now go with the None 
i.	For DNS options, clear Enable DNS hostnames.
j.	Choose Create VPC.
<img width="960" alt="image" src="https://github.com/user-attachments/assets/d42e7a19-e9c4-4cbc-ba7f-aaa0278573a7">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/da629b3f-34a6-4cdb-ac59-980b115c3542">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/69004536-7b60-47ea-bc47-fdcb190a522a">
k.Now, we successfully created the vpc.

### <p align="">Step2:</p>
  
### **Creating the Auto Scaling Group :**
  
1. First create the Launch template
<img width="960" alt="image" src="https://github.com/user-attachments/assets/e99b40a8-8910-4e27-b26d-bbb2e67a9bda">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/b1a7c7e4-b892-494a-9270-29c76cfcc32c">
2. Next select the key pair which is in the form of .pem file
<img width="960" alt="image" src="https://github.com/user-attachments/assets/5a95e8ea-90d8-4820-a4b6-7c72d5afd49a">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/377b1630-0141-496b-82d4-d1599a2f99ec">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/4e82ae2e-4da3-42d4-90dc-487306f97c69">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/d20f0185-9552-4167-bc41-e0e3feade1a1">
3. After selecting the all correct details, Click on 'create Launch template'
4. <img width="960" alt="image" src="https://github.com/user-attachments/assets/f949f122-7fc0-459a-a3e0-62577cc6ec56">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/1b064909-af69-4092-b4c4-22c53afaedde">
5. Scroll Down and then Click "Next".
<img width="960" alt="image" src="https://github.com/user-attachments/assets/64228bf7-b401-41cb-b6b5-ca2052b7dfd4">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/85f7fb43-eef2-4b1b-b47f-d1428ddf4d3b">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/548c868f-8ceb-4260-95ea-c6b32a646789">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/df08d697-676e-40b8-8b85-3e1721cca7b4">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/a07f6d70-e317-4781-b1e8-bb097edab19a">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/b367a901-c2b5-4474-b70c-ea6da609da1d">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/fa7c2eac-53e2-4f58-b875-51c284c30e54">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/601252b1-547e-46e4-9cf2-0402ce9c2cab">
6. Click on 'create Auto scaling group'.
<img width="960" alt="image" src="https://github.com/user-attachments/assets/244f29b3-2c94-4649-ba25-5f09bb6ce03d">
7. Now your are Successfully Created Auto Scaling Group.
8. Look for the instances created by your Auto Scaling Group.
Since you mentioned that the Auto Scaling Group launched instances in different Availabilty Zones, you can check the "Availability Zone" column to verify that these instances are indeed distributed across multiple Availability Zones.

### <p align="">Step 3:</p>
  

###  Creating the Bastion Host :    
 Launch Instance as Specified below .
<img width="960" alt="image" src="https://github.com/user-attachments/assets/d55fa6d5-b130-4ddd-9fcd-cbc86d5cff7d">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/562e95a3-12f8-4841-ab4b-415d17cea7ed">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/d23a4f78-66d3-428c-976a-3dba172101bd">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/554f8a6b-2d2e-4ed3-81aa-d1101213521e">
Bastion Host should be created in same vpc.
<img width="960" alt="image" src="https://github.com/user-attachments/assets/fe065293-93df-4d2b-885a-b58b4ceaeb20">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/501d59d1-7da0-4979-9ebc-6e928584b6dd">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/1fca6c8a-9b83-45f9-bb2a-eed1547eb200">

### <p align="">Steps 4:</p>
  

#### <p align="">SSH into Private Instance</p>

###     
1. SSH into the Bastion Host Instance: To SSH into the private instances, we first need to connect to our Bastion host instance. From there, we'll be able to SSH into the private instance.
2. Ensure the PEM File is Present on the Bastion Host: Additionally, make sure that the PEM file is present on the Bastion host. Without it, you won't be able to SSH into the private instance from the Bastion host.
3. Open a putty terminal on your local machine.
4. Execute the Following Commands: 

   a. Save the keypair pem file using vim editor, Example:
   ```bash
   vim prod_kp
   ``` 
   b. Give the read permission to that pem file. Like,
   
   ```bash
   chmod 400 prod_kp
   ``` 
   If you are using ubuntu then,
   Copy the PEM file to the Bastion host using the ```scp``` command. Replace <pem file location> with the local 
   and remote file paths, and <bastion host public IP> with 
   the Bastion host's public IP address. Example:

   ``` bash
   scp -i /Users/khadharbee/Downloads/prod_kp.pem 
   /Users/khadharbee/Downloads/prod_kp.pem  
   ubuntu@10.0.18.8:/home/ubuntu
   ```

   c. After SSHing into the Bastion host, use the ls command 
   to check if the ``` prod_kp.pem``` file is present. If it's not 
   there, double-check your previous commands. Now, you 
   can SSH into the private instance using the following 
   command, replacing < private IP> with the private 
   instance's IP address:

   ``` bash
   ssh -i prod_kp.pem ubuntu@<private IP>
   ```
   
   <img width="960" alt="image" src="https://github.com/user-attachments/assets/0a7c1590-a2ea-46a3-9605-fd58e537eedf">

   d. We will deploy our application on one of the private 
   instances to test the load balancer. After successfully 
   SSHing into the private instance, create an HTML file 
   using the Vim text editor:

   ``` bash
   vim index.html
   ```
   e. This will open the Vim editor. Copy and paste any HTML 
   content you like into the editor. For example:
   ``` bash
   <html>
   <head>
   <title>Page Title</title>
   </head>
   <body>

   <h1>This is my first project to demonstrate apps in private subnets</h1>
   </body>
   </html>
   ```
   f. After pasting the content, save the file by pressing 'Esc' 
   to exit insert mode and then entering ':w' to save. Finally, 
   start a Python HTTP server on port 8000 to deploy your 
   application on the private instance:
   ``` bash
   python3 -m http.server 8000
   ```
Now, your application is deployed on the private instance on port 8000.

### Note :
We intentionally deployed the application on only one instance to check if the Load Balancer will distribute 50% of the traffic to one instance (which will receive a response) and 50% to another instance (which will not receive a response).

### Step 4:
 #### Creating the Load Balancer :
1. Access the EC2 Terminal.
2. Before creating Load Balancer, First create Target Group. For creating Target Group follow the steps below.
<img width="960" alt="image" src="https://github.com/user-attachments/assets/968e2ade-c20a-4fac-b144-2e905c56b464">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/7ea79c01-2bd5-44dd-8a94-41df3bd6dba2">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/dcb69ba9-4312-4ba4-86b2-a863e7180a10">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/ac171b14-b355-4c40-8bf4-590766d6e01b">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/97e582f1-6692-45a5-8ab0-f72b3f8548ba">
3.Now, Start create the Load Balancer.
4. Follow the below steps.
<img width="960" alt="image" src="https://github.com/user-attachments/assets/ed37ea2f-a18c-42fb-be06-40f995e0aa9d">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/d8e198bf-949d-40ec-a54c-69ee30f51b0d">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/d4fde067-740e-46ab-8afd-561fdf12e004">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/7f466cdc-c4a7-4e25-b885-1ad5ca1ada08">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/28d7d2e6-2996-4143-b2f4-ac88291501ce">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/55a3ed87-11ca-44b9-9b58-919ff5c0feda">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/a32c2c45-4f74-4e4d-b28a-81be4829b7e4">
5. Now, we successfully created the Load Balancer.
6. We allowed port 8000 in security group Inbound rule but not port 80 which we given in Load Balancer. So it show error like this:
<img width="960" alt="image" src="https://github.com/user-attachments/assets/a50fe213-b453-484a-9011-35c73914afaa">
7. So, Add and save the port 80 rule in Inbound rule section. Then Not reachable turn to the reachable in green colour.
<img width="960" alt="image" src="https://github.com/user-attachments/assets/472a43f7-b5e9-45b7-95c8-4b6ac8a8ec93"> 
8. As all the steps completed, Copy DNS name & paste it in browser to access website from first EC2 instance
<img width="960" alt="image" src="https://github.com/user-attachments/assets/1279a22f-ce29-4d47-8b80-951d15ec6b7a">
<img width="960" alt="image" src="https://github.com/user-attachments/assets/f02371ff-8be4-4aba-9f96-d8370a3887df">
Now We Successfully deployed Application securely in Private instance.

  

  
          

    

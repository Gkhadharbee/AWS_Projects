
# <p align="center">VPC with servers in private subnets and NAT Gateway
## <p align="">About the project</p>
  This example demonstrates how to create a VPC that you can use for servers in a production environment.
To improve resiliency, you deploy the servers in two availability zones, by using an Auto Scaling group and an Application Load Balancer. For additional security, you deploy the servers in private subnets. The servers receive requests through the load balancer. The servers can connect to the internet by using a NAT gateway in both Availability Zones.
![](https://docs.aws.amazon.com/images/vpc/latest/userguide/images/vpc-example-private-subnets.png)

## <p align="">Steps</p>
  

### <p align="">Step1:</p>
  
Create the VPC :
Open the Amazon VPC console by visiting https://console.aws.amazon.com/vpc/.
On the dashboard, click on "Create VPC."
Under "Resources to create," select "VPC and more."
Configure the VPC:

a. Provide a name for the VPC in the "Name tag auto-generation" field.     
b. For the IPv4 CIDR block, leave it as default suggestion.

Configure the subnets:    
a. Set the "Number of Availability Zones" to 2 for increased resiliency across multiple Availability Zones.    
b. Specify the "Number of public subnets" as 2.    
c. Specify the "Number of private subnets" as 2.    
d. For NAT gateways, choose "1 per AZ" to enhance resiliency.    
g. For VPC endpoints, you can choose "None" .    
h. Regarding DNS options, clear the checkbox for "Enable DNS hostnames."    
Once you've configured all the settings, click "Create VPC."
i.Now, we successfully created the vpc.

### <p align="">Step2:</p>
  
### **Creating the Auto Scaling Group :**
  
1. First create the Launch template
2. Next select the key pair which is in the form of .pem file
3. After selecting the all correct details, Click on 'create Launch template'
4. Scroll Down and then Click "Next".
5. Click on 'create Auto scaling group'.
6.  Now your are Successfully Created Auto Scaling Group.
7. Look for the instances created by your Auto Scaling Group.
Since you mentioned that the Auto Scaling Group launched instances in different Availabilty Zones, you can check the "Availability Zone" column to verify that these instances are indeed distributed across multiple Availability Zones.

### <p align="">Step 3:</p>
  

###  Creating the Bastion Host :    
 Launch Instance as Specified below .

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
   c. Give the read permission to that pem file. Like,
   
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

   d. After SSHing into the Bastion host, use the ls command 
   to check if the ``` prod_kp.pem``` file is present. If it's not 
   there, double-check your previous commands. Now, you 
   can SSH into the private instance using the following 
   command, replacing < private IP> with the private 
   instance's IP address:

   ``` bash
   ssh -i prod_kp.pem ubuntu@<private IP>
   ```

   e. We will deploy our application on one of the private 
   instances to test the load balancer. After successfully 
   SSHing into the private instance, create an HTML file 
   using the Vim text editor:

   ``` bash
   vim index.html
   ```
   f. This will open the Vim editor. Copy and paste any HTML 
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
   g. After pasting the content, save the file by pressing 'Esc' 
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
2. Follow the below steps.
3. Copy DNS name & paste it in browser to access website from first EC2 instance

Now We Successfully deployed Application securely in Private instance.

  

  
          

    
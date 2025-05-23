# Creating AWS VPC Flow Logs and Generating Traffic
### Architecture
![task_id_142__creating_vpc_flow_logs_and_generating_traffic](https://github.com/user-attachments/assets/a77bc1d5-bdea-4760-988e-086df6e58f44)
### Project Details
1. Create CloudWatch Logs.
2. Create a VPC.
3. Create an Internet Gateway.
4. Create a Subnet.
5. Create VPC Flow Logs.
6. Create an EC2 Instance.
7. Generating Traffic
8. Viewing log events in CloudWatch Log groups.
### Project Steps
1. Create CloudWatch Logs
- Navigate to the Services menu at the top and choose CloudWatch under Management and Governance.
- Click on Log Groups on the left side panel and Click on Create log group button
- Enter the Log Group Name:
2. Create a VPC.
- VPC Only : MyVPC 
- 10.1.0.0/16
![3_29_20](https://github.com/user-attachments/assets/1bcfcaeb-d5ab-458b-bde3-33e960f50d24)
- Then leave the other fields as default and click on Create VPC
3. Create an Internet Gateway.
- Select Internet Gateways on the left side panel and click on the Create internet gateway  
- Enter the name as MyInternetGateway. Leave everything else as default and click on the Create internet gateway
![5_31_57](https://github.com/user-attachments/assets/9243fc00-3b71-42d3-8f9d-843ae682f439)
- Once created, attach it to MyVPC by clicking on Actions at the top and selecting Attach to VPC.
![6_33_03](https://github.com/user-attachments/assets/2ac60d28-8335-435f-a523-18d8861a596e)
- Under Available VPCs, select MyVPC and then click on Attach internet gateway button.
- Click on the Route Tables on the left side panel and then select the main route table for your VPC, i.e., MyVPC.
- Now click on the Routes tab and then click on Edit routes.
![7_35_33](https://github.com/user-attachments/assets/f68ddf27-182f-4fa8-aae6-21d5222cf3ae)
- Click on Add Route :0.0.0.0/0 InternetGateway
![8_36_57](https://github.com/user-attachments/assets/1ced69b1-b2c1-4e8f-8433-2f3089d48bb1)

4. Create a Subnet.
- Subnet 1 :  10.1.1.0/24 US East(N.Virginia)/us-east-1a
5. Create VPC Flow Logs.
- CloudWatch with role VPCFlowLog_Role
6. Create an EC2 Instance.
- t2. micro
- Linux 2
- Public subnet
- VPCFlowLog_Role
- SG : Inbound SSH, HTTP
7. Generating Traffic
- After SSH to EC2
- This command allows you to switch to the superuser or root user. 
```
sudo su
```
- This command updates the packages and software on the EC2 instance.
```
yum -y update
```
- This command installs the Apache HTTP Server, commonly known as Apache. Apache is a widely used web server software that enables the hosting of websites and serves web content.
```
yum install httpd -y
```
- This command changes the current directory to the default location where web content is served by Apache.
```
cd /var/www/html
```
- This command creates a simple HTML file named “index.html” and sets its content as “Response coming from server”.
```
echo "Response coming from server" > /var/www/html/index.html
```
- This command starts the Apache web server service
```
systemctl start httpd
systemctl enable httpd
systemctl status httpd
```
- Copy your instance's Public-IP/index.html, paste it into your browser and hit enter.
![public-ip-index](https://github.com/user-attachments/assets/49a7de8c-dc2b-4085-a1d5-5fdd78d208a4)
8. Viewing log events in CloudWatch Log groups.
![log_events](https://github.com/user-attachments/assets/609e80db-0e75-40c2-944b-519837194ecb)


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

5. Create a Subnet.
6. Create VPC Flow Logs.
7. Create an EC2 Instance.
8. Generating Traffic
9. Viewing log events in CloudWatch Log groups.

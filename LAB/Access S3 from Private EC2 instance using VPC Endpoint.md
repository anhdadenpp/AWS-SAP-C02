# Access S3 from Private EC2 instance using VPC Endpoint
## Architecture
![a](https://github.com/user-attachments/assets/49940f55-ca31-4793-94f4-deb0bdf2f5d6)
## Project Details
### Step 1 : Sign in to AWS Management Console
### Step 2 : Create a VPC
1. Region : N. Virginia
2. Create VPC Only
-  Name tag : MyVPC
-  IPv4 CIDR : 192.168.0.0/26
-  No IPv6
-  Tenancy : Default
### Step 3 : Create and attach an Internet Gateway with custom VPC
-  Create Internet Gateway : MyInternetGateway
-  Attach to VPC
### Step 4 : reate a Public and Private Subnet
-  Public Subnet : Public subnet, us-east-1a, 192.168.0.1/27
-  Private Subnet: Private subnet, us-east-1b, 192.168.0.32/27
### Step 5 : Configure the Public subnet to enable auto-assign public IPv4 address
- Select Public Subnet -> Edit subnet settings -> Enable auto-assign public IPv4 address under Auto-assign IP settings
### Step 6 : Create a Route Table 
1. Route table for Public Subnet
- Name : PublicRouteTable
- VPC : MyVPC
- Subnet Associations : Public subnet
- Routes -> Edit routes -> Add routes :
+ Destination : 0.0.0.0/0
+ Target : MyInternetGateway
2. Route table for Private Subnet
- Name : PublicRouteTable
- VPC : MyVPC
- Subnet Associations : Private subnet
### Step 7 : Create Sercurity groups


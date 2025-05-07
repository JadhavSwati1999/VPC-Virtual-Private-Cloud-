# VPC-Virtual-Private-Cloud.
Virtual-private-cloud
A virtual private cloud (VPC) is **a virtual network dedicated to your AWS account**. It is logically isolated from other virtual networks in the AWS Cloud. You can specify an IP address range for the VPC, add subnets, add gateways, and associate security groups.

## Key Components of VPC.

**IGW(Internet Gate Way):**  *An Internet Gateway (IGW) is an AWS component that provides a path for network traffic to travel between a Virtual Private Cloud (VPC) and the public internet.*

**Subnets:**  A *subnet* is a range of IP addresses in your VPC. You launch AWS resources, such as Amazon EC2 instances, into your subnets. You can connect a subnet to the internet, other VPCs, and your own data centers, and route traffic to and from your subnets using route tables.

**Route Tables:**  A *route table* contains a set of rules, called *routes*, that determine where network traffic from your subnet or gateway is directed.

**NAT Gateway(Network Address Translation):**  *A NAT gateway is a Network Address Translation (NAT) service. You can use a NAT gateway so that instances in a private subnet can connect to services outside your VPC but external services cannot initiate a connection with those instances.*

**NACL (Network Access Control List):** A *network access control list (ACL)* allows or denies specific inbound or outbound traffic at the subnet level.

**Security Group:** *A security group controls the traffic that is allowed to reach and leave the resources that it is associated with.*

### What is Bastion Host?


A Bastion host is a special-purpose server or an instance that is used to configure to work against the attacks or threats. It is also known as the ‘jump box’ that acts like a proxy server and allows the client machines to connect to the remote server. It is basically a gateway between the private subnet and the internet. It allows the user to connect private network from an external network and act as  proxy to other instances. 

# Create A Secure VPC

## Step 1: Login Into The AWS Account

1. Login into the AWS account using  login credentials.

## Step 2: Create VPC

1. Search VPC  service in the search bar.


1. VPC Dashboard where we can create a VPC , Click on the ***create VPC*** 


1. Select VPC only  while creating VPC 

## Step 3: VPC settings

1. Give a name to the VPC.
2. Assign IPv4 CIDR range between /16 and /28


1. Click on Create VPC


1. VPC is Successfully created


## Step 4 : Create  IGW

1. Create IGW click on create Internet gateway


1. Create internet gateway Settings
2. Give a Name in Name tag and Click on Create internet gateway.


1. Internet gateway is successfully created



## Step 5 : Attach IGW(Internet gateway) to VPC

1. Attach to VPC


1. Select the VPC 


1. Internet gateway is successfully attached to the VPC

## Step 6 : Create Subnets

1. Create a subnet click on Create subnet


1. select VPC


1. Give a name to the Subnet



1. Subnet Settings



1. Give name , select Availability Zone , and Provide IPv4 CIDR 


1. The Subnet is created 


1. Create one more subnet as Private-Sub
2. Give name ,availability zone , IPv4 CIDR


1. Two subnets are created as Public-sub and Private-sub


## Step 7: Create NAT gateway

1. Create NAT gateway , click on Create NAT gateway


1. Create NAT gateway settings



1. Give a name in Name tag 
2. Select subnet 
3. Allocate Elastic IP 
4. Click on create NAT gateway



1. NAT gateway is successfully created.



## Step 8: Create Route Table

1. Create a route table
2. Click on Create route table 


1. Create route table assign name 
2. Select VPC 
3. Create route table


1. Public route table is successfully created



1.  Two Route tables are created Public-route-table and Private-route-table



## Step 9: Edit routes to the created Route tables

1. Select the Public-Route-Table first
2. Click on Actions and select Edit routes  


1. Select Anywhere (0.0.0.0/0) in destination 
2. In target select Internet Gateway and select the IGW


1. Update routes for Public route table



1. Now edit routes for Private-route table



1. Select anywhere in destination and select the NAT gateway in target



## Step 10: Associate Route table to subnets

1. Associate the Private route table to private subnet


1. Associate Public route table to public subnet



1. Route tables are successfully associated with the subnets


## Step 11 : Create NACLs(Network access control list)

1.Create a Private NACL 


1. Assign a the default NACL as public NACL  


1. Select the Private NACL
2. Click on Actions and Select Edit subnet associations 


1. Associate the Private NACL to private subnet
2. Associate the Public NACL to public subnet 


1. NACLs are successfully associated with the subnets.


## Step 11: Launch EC2 instances

1. Launch instance



1. Click on launch instances


1. Launch an instances with the name Bastion . 



1. Assign the appropriate key 



1. Select the VPC and the  public subnet
2. Enable the auto assign public IP
3. configure security group (Allow SSH traffic port: 22)



1. Select the source type (anywhere, My IP, custom IP ) according to you 



1. Configure HTTP rule in the inbound rule


1. Instance is successfully created 
2. Like-wise create one more instance in Private Subnet with name Database


## Step 12 : Edit NACL Inbound & Outbound rule

1. Assign inbound and outbound NACL
2. select private NACL 


1. Assign rule no as 100 and assign the inbound role that you want to configure
2. Click on save changes


1. Assign outbound rules


1. The now to check the inbound and outbound rule in the security group of the instances


1. Select the bastion instance created for public subnet


1. Check the inbound rules into the security group of the bastion instance 



1. Check the outbound rules into the security group of the bastion instance



1. Now select the Database Instance created for the private subnet



1. Check the inbound and outbound rules for the database instance 


# Step 13: Successful login to bastion server

1. Successfully logged in to the bastion server(created in public subnet)



```jsx
Note: You can also access the database server from the bastion host.
```

# Summary

To take access of EC2 Instance(Bastion Server) created in a VPC Network under which there were two subnets(Public & Private) . In which resources(EC2) were created. 

To take that access first we created a VPC, created two subnet under it, one internet gateway and NAT gateway create route tables and configure then assign to the subnets . Create private NACL and attach to private subnet. Create two instances under public and private subnets accordingly .Configure security group for private subnet instances .

Access Bastion Host from your local machine.

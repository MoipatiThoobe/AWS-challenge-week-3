# AWS-challenge-week-3
Week 3 of the 12 weeks of AWS challenge

The third week of the challenge focused of Networking, in AWS networking in done using Amazon Virtual Private Cloud (Amazon VPC). Amazon VPC lets you provision a logically isolated section of the AWS Cloud where you can launch AWS resources in a virtual network that you define. You have complete control over your networking environment, including selection of your own IP address range, creation of subnets and configuration of route tables and network gateways. 

## VPC fundamentals
Amazon VPC enables you to launch AWS resources into a virtual network that you have defined.

In the hands on lab, I will be doing the following:
* Set up a VPC with public and private subnets
* Connect the VPC to the internet
* Establish private connections to AWS resources

### Prerequisite steps
* Create a stack on CloudFormation using the prerequisites.yaml CloudFormation template. The template with create the following resources:
  * An IAM role for the EC2 instances
  * EC2 instance profile to define the IAM role that the EC2 instances should use
  * IAM role for VPC Flow logs
  * An S3 bucket that will be used to test VPC Endpoints

1. Create a VPC 

<img width="954" alt="1" src="https://github.com/user-attachments/assets/c132d68b-7d9b-4440-b664-386f7c4093ce" />

2. enable **DNS resolution** and enable **DNS hostnames**

<img width="950" alt="2" src="https://github.com/user-attachments/assets/b1e7eb7b-4939-4200-8be0-b8a857ce790b" />

3. Create two public and private subnets in two availability zones within the VPC. A subnet is a range of IP addresses inside of the VPC. 

<img width="956" alt="4" src="https://github.com/user-attachments/assets/52910800-d209-4649-bb93-869409ade83f" />

<img width="958" alt="5" src="https://github.com/user-attachments/assets/a8fd872a-cd92-48ff-ae1a-7281348ef035" />

<img width="956" alt="6" src="https://github.com/user-attachments/assets/1a930e69-6607-45d3-b17c-d6aced4fe0f2" />

<img width="958" alt="7" src="https://github.com/user-attachments/assets/c2337f8f-91ef-4a91-9092-064a85ebfdda" />

4. Create a network control list (NACL) for the subnets. A NACL is an optional layer of security for the VPC for controlling traffic in and out of one or more subnets.

<img width="959" alt="8" src="https://github.com/user-attachments/assets/c0530efb-98ad-4812-b598-f306c755ad42" />

5. Update the subnet associations in the NACL and update the inbound/outbound rules

<img width="955" alt="9" src="https://github.com/user-attachments/assets/a8d58d4c-96fa-4fcf-a7d8-4052ed1feb12" />

<img width="956" alt="10" src="https://github.com/user-attachments/assets/88fa3996-a7c5-4693-a16b-8d0db819c611" />

<img width="951" alt="11" src="https://github.com/user-attachments/assets/f9d17aa6-0c16-4554-8e64-bd522f0ff87a" />

6. Create a public and private route table for the subnets. Each subnet inside of the VPC must be associated with a route table, which controls the routing for the subnet (subnet route table).

<img width="952" alt="12" src="https://github.com/user-attachments/assets/6438d65f-d3ba-447c-b553-bae7c189543f" />

<img width="956" alt="14" src="https://github.com/user-attachments/assets/d4b5cc02-3d77-4020-a00d-fe3f2c0b9bc6" />

7. Associate the subnets with the public and private route tables

<img width="955" alt="13" src="https://github.com/user-attachments/assets/599f9106-5e26-490d-81c3-c3dd84ce5181" />

<img width="956" alt="15" src="https://github.com/user-attachments/assets/67ad9c05-33f0-4fee-b67e-edd3b3dd04db" />

8. Deploy an Internet Gateway (IGW), an Internet Gateway establishes outside connectivity for EC2 instances that will be deployed inside of the VPC.

<img width="957" alt="16" src="https://github.com/user-attachments/assets/805b1fa1-e8fd-49e4-b6bb-744a79bec08f" />

9. Attach the IGW to the VPC

<img width="953" alt="17" src="https://github.com/user-attachments/assets/68cb327e-e309-48c9-ac7f-6d6fdbad0cd9" />

10. Update the VPC routing tables to point the default routes for the public subnets to the IGW

<img width="954" alt="18" src="https://github.com/user-attachments/assets/77f1eca5-00bb-4ef4-a968-f56e0eadb74b" />

11. Create a NAT gateway. A NAT gateway provides outbound connectivity for workloads running in private subnets.

<img width="954" alt="19" src="https://github.com/user-attachments/assets/c5c93e43-fe3e-42d3-8845-d5d2e2635aa6" />

12. Now that there is a NAT gateway we need to update the route tables for the private subnets to create a route it

<img width="958" alt="20" src="https://github.com/user-attachments/assets/d3df1ea2-bc02-42e8-a960-c7ea2f82f2c9" />

13. Create a interface endpoint for KMS. Interface endpoints create a network interface inside the VPC's subnets, all traffic to the service flows through this interface to the service.

<img width="954" alt="21" src="https://github.com/user-attachments/assets/a6d6a49a-149d-479b-baac-4e71093a0bf0" />

14. Create a gateway endpoint for S3. Gateway endpoints only support S3 and DynamoDB, they reach these services through a gateway from the VPC.

<img width="954" alt="22" src="https://github.com/user-attachments/assets/e2c1d0f8-bc35-4b37-9eb2-3abb3081a854" />

15. Launch an EC2 instances into a public and private subnet

<img width="954" alt="23" src="https://github.com/user-attachments/assets/cd9f05db-d59e-43d5-936b-1207765f1e90" />

<img width="959" alt="24" src="https://github.com/user-attachments/assets/f8fc4238-f640-4832-ad81-d78620db09c0" />

16. Ping the Elastic IP of the Public EC2 instance from the Command line terminal. This confirms that there is connectivity between the public EC2 instance and the internet.

<img width="312" alt="25" src="https://github.com/user-attachments/assets/03de84d8-0056-4372-a5b9-d25686fb81ee" />

17. Use Session manager to connect to the Private EC2 instance. Test the connectivity by pinging both the public instance and example.com.

<img width="770" alt="26" src="https://github.com/user-attachments/assets/8d600ea3-c357-43a8-969c-68a52be37964" />

18. The following command is used to check the DNS for the KMS service from the VPC A instance

<img width="461" alt="27" src="https://github.com/user-attachments/assets/a9107af9-b04f-4aef-b36a-a2b5db47e4d8" />

19. Clean up resources to avoid incurring costs:

19.1 Terminate the EC2 instances

19.2 Delete the VPC endpoints

19.3 Delete the VPC

19.4 Delete the Prerequisites CloudFormation Stack

## Multiple VPCs

A VPC peering connection is a networking connection two VPCs that enables you to route traffic between them using IPV4 addresses or IPV6 addresses. AWS Transit Gateway is a service that enables you to connect VPCs and on=premises networks to a single gateway. 

In this hands on lab, I will do the following: 
* Peer multiple VPcs
* Create a Transit Gateway, attach VPCs and configure routing with the Transit Gateway route tables

### Prerequisite steps
* Create a stack on CloudFormation using the prerequisites.yaml CloudFormation template.

  <img width="952" alt="1" src="https://github.com/user-attachments/assets/fd3b9d71-dc3b-4b6f-8cd8-e2d0165354e0" />

* Create a stack on CloudFormation using the multi-vpc-create-all-vpcs template. The template will create the following resources:
  * Three VPCS
  * Each VPC has two public and two private subnets
  * Each VPC has an EC2 instance in the private subnet
  
  <img width="956" alt="2" src="https://github.com/user-attachments/assets/0d5a3c16-3e70-4cfd-9702-3f78f0240ef1" />

1. Create a peering connection between VPC A and VPC B. A VPC peering connection is a networking connection between two VPCs that enables you to route traffic between them using private IPV4 or private IPV6 addresses.

<img width="949" alt="3" src="https://github.com/user-attachments/assets/50234303-a87c-415b-ad49-292828b15759" />

<img width="953" alt="4" src="https://github.com/user-attachments/assets/b4cbb9ac-797d-4160-9d69-3dc6a3ecc6ce" />

2. Update the route table in VPC A, add a route entry for VPC B using its CIDR range 

<img width="954" alt="5" src="https://github.com/user-attachments/assets/9a7f25ed-9ce8-4c79-9efc-05affdd4b7f6" />

3. Update the route table in VPC B, add a route entry for VPC A using its CIDR range

<img width="954" alt="6" src="https://github.com/user-attachments/assets/e951e6b9-dfce-421d-9631-e3fbfdab03e5" />

4. Create a peering connection between VPC A and VPC C

<img width="959" alt="7" src="https://github.com/user-attachments/assets/92b12378-4ace-4312-b8d1-decd4fac6fd7" />

5. Update the route table in VPC A, add a route entry for VPC C using its CIDR range

<img width="953" alt="8" src="https://github.com/user-attachments/assets/a07c1dac-da51-4540-8994-f1096aa5a060" />

6. Update the route table in VPC C, add a route entry for VPC A using its CIDR range

<img width="956" alt="9" src="https://github.com/user-attachments/assets/45e98bde-96c1-4f99-8a6a-3b5b9222a49e" />

7. Connect to the VPC A AZ1 Server EC2 instance using Session manager and ping the instances in VPC B and VPC C using their private addresses. We are receiving results which confirms that we have peered and routed correctly. Terminate the session manager connection when finished.

<img width="422" alt="10" src="https://github.com/user-attachments/assets/3f49d054-774c-4a3b-ad33-71727d11bce8" />

8. Connect to the VPC B AZ1 Server EC2 instance using Session manager and ping the instance in VPC A

<img width="409" alt="11" src="https://github.com/user-attachments/assets/0c0cb6e7-5fcd-4a71-8109-9d7b06573148" />

9. We do not get any data when we try to ping the instance in VPC C because there is no peering connection between the VPC B and VPC C

<img width="431" alt="12" src="https://github.com/user-attachments/assets/542c632d-1cf1-46fe-9f33-bc4e6e7d172d" />

10. Delete the VPC peering connections amd delete the related route table entries

11. Create a transit gateway. AWS Transit Gateway connects your VPCs and on-premises networks through a central hub

<img width="959" alt="1" src="https://github.com/user-attachments/assets/ef304d95-5ee4-49f8-ae54-691fe9a7f3dd" />

12. Create Transit Gateway Subnets in VPC A

<img width="954" alt="2" src="https://github.com/user-attachments/assets/e765e1d4-0752-4dc2-ba58-acbe96216a79" />

<img width="952" alt="3" src="https://github.com/user-attachments/assets/169cfb0f-932c-49d4-aa1a-d090a352f54b" />

13. Create Transit Gateway Attachments for VPC A, B and C

<img width="958" alt="4" src="https://github.com/user-attachments/assets/ad395aae-f12f-457c-9115-d692b21fb51e" />

<img width="956" alt="5" src="https://github.com/user-attachments/assets/59ef083d-a8ad-4292-aead-387fcf7d8a3c" />

<img width="955" alt="6" src="https://github.com/user-attachments/assets/ba05b169-63c3-4705-b2f8-6488b7631f55" />

14. Add routes to Transit Gateway in the VPC Route Tables

<img width="953" alt="7" src="https://github.com/user-attachments/assets/d94a31c1-968f-4923-b212-74f362f217d0" />

<img width="952" alt="8" src="https://github.com/user-attachments/assets/4be274b8-a3de-4fb3-8281-79f5301726e9" />

<img width="946" alt="9" src="https://github.com/user-attachments/assets/95c08e3c-0425-4d54-bf05-52c2d59485d2" />

15.  Connect to the VPC A AZ1 Server EC2 instance using Session manager and ping the instances in VPC B and VPC C using their IP addresses. A response from both instances confirms that the Transit Gateway has been set up correctly.

<img width="416" alt="10" src="https://github.com/user-attachments/assets/724f8082-5258-482f-b73b-289ae8632e75" />

16. Delete VPC A Attachment from Transit Gateway Route Table

<img width="958" alt="1" src="https://github.com/user-attachments/assets/9a1b8d52-64fb-4e94-a283-25c8caae5463" />

17. Delete propagations for VPC B and VPC C from Transit Gateway Route Table

<img width="954" alt="2" src="https://github.com/user-attachments/assets/58579c51-ba59-4854-98aa-e8766f461b6a" />

<img width="956" alt="3" src="https://github.com/user-attachments/assets/bb29f1ff-11a6-4d4f-9c4e-80d8faf86cbd" />

18. Create a shared services route table

<img width="950" alt="5" src="https://github.com/user-attachments/assets/66b40e97-93c8-4bc1-a3a1-141bbc13aa78" />

19. Associate VPC A attachment with the shared services route table

<img width="953" alt="6" src="https://github.com/user-attachments/assets/0134fa33-6b7a-4892-8625-7491458e148c" />

20. Create Propagations for VPC B and VPC C

<img width="959" alt="7" src="https://github.com/user-attachments/assets/bae445f4-6891-42f1-ac33-d40002337661" />

<img width="956" alt="8" src="https://github.com/user-attachments/assets/4bf4ec26-0e2d-43eb-80b3-314a3d9b1552" />

<img width="836" alt="9" src="https://github.com/user-attachments/assets/541d2e68-3ff3-4ff7-8ebc-1e716a6d0756" />

21. Use Session manager to connect to the EC2 instance in VPC B and test connectivity to the instances in VPC A and VPC C

<img width="430" alt="10" src="https://github.com/user-attachments/assets/a7c52d97-604e-43d5-b6e7-1d5e95fbc560" />

22. Clean up resources

22.1 Delete the transit gateway attachments and then delete the transit gateway

22.2 Delete the MultiVPC and Prerequisite cloudformation stacks

## Security controls
Security in VPCs can be managed using the following:
* Network ACLs: stateless access controls that you configure at a subnet level, to allow or block a CIDR block on a particular port or range of ports. Network ACL rules are a numbered list and are evaluated top down, with a DENY ALL at the end. Both in inbound and outbound traffic can be controlled with these rules.
* Security groups: virtual, stateful firewall attached to an instance or a network interface. Both inbound and outbound rules can be defined to allow specific protocols, ports and source/destination CIDR. A DENY is not possible with security groups.
* Endpoint policies are IAM policies attached to VPC endpoints to restrict/grant permission to the service's API calls.

In the hands on lab, I will be doing the following:
* Modify the Network ACL associated with the workload subnets in VPC A to only ICMP traffic from VPC B's CIDR
* Modify the security group attached to VPC A private EC2 instance to allow only ICMP traffic inbound from VPC C's CIDR only
* Modify the S3 endpoint policy to limit read only access to S3 buckets within the VPC

### Prerequisite steps
* Create a stack on CloudFormation using the prerequisites.yaml CloudFormation template. 

<img width="952" alt="1" src="https://github.com/user-attachments/assets/fd3b9d71-dc3b-4b6f-8cd8-e2d0165354e0" />

* Create a stack on CloudFormation using the multi-vpc-create-all-vpcs-and-tgw template. The template will create the following resources:
  * Three VPCS
  * Each VPC has two public and two private subnets
  * A Transit gateway to provide connectivity between the VPCs
  * Each VPC has an EC2 instance in the private subnet

  <img width="950" alt="2" src="https://github.com/user-attachments/assets/10fc882c-cc4d-4807-8dfa-ac7a73b8e87d" />

1. Select the VPC A Workload Subnets NACL and modify the first rule (100) to allow only ICMP traffic from VPC B's CIDR. All other traffic will be denied by the catch-all DENY rule
 
<img width="952" alt="3" src="https://github.com/user-attachments/assets/0339282c-27de-411b-aa45-0c161844aea1" />

2. Connect to the EC2 instance in VPC B using EC2 session manager and verify reachability to the EC2 instance in VPC A by pinging the instance using its IP address, the traffic will flow through successfully because we modified the NACL. Terminate the session when finished.

<img width="427" alt="4" src="https://github.com/user-attachments/assets/d7dc1f36-b937-4725-a78b-1a771d138dac" />

3. Connect to the EC2 instance in VPC C using EC2 session manager and verify reachability to the EC2 instance in VPC A by pinging the instance using its IP address, the traffic will not flow through because the NACL in VPC A is denying all ICMP traffic that does not come from VPC B. 

<img width="428" alt="5" src="https://github.com/user-attachments/assets/ea5b291a-455c-4133-94c3-ff250a5c6747" />

4. Select the VPC A Workload Subnets ACL and modify the first rule to allow all traffic from anywhere

<img width="950" alt="6" src="https://github.com/user-attachments/assets/898aae0d-9db5-46f9-acec-9eb59625bae0" />

5. Select the VPC A Private AZ1 Server EC2 instance and modify the security group to allow only from VPC C's CIDR

<img width="958" alt="7" src="https://github.com/user-attachments/assets/332fb90c-27c3-45c3-af74-ffb795706dcb" />

6. Connect to the EC2 instance in VPC A using EC2 session manager and verify reachability to the EC2 instance in VPC B by pinging the instance using its IP address

<img width="428" alt="5" src="https://github.com/user-attachments/assets/ce57a353-a6af-4808-82c6-7bf6ed429144" />

7. Connect to the EC2 instance in VPC C using EC2 session manager and verify reachability to the EC2 instance in VPC A by pinging the instance using its IP address, traffic will flow through because the security group on the EC2 instance in VPC A is allowing ICMP traffic from VPC C's CIDR range. Terminate the session when finished.

<img width="419" alt="8" src="https://github.com/user-attachments/assets/5cbd00d2-564e-4280-ae10-023e52955a29" />

8. Select VPC A Private AZ1 Server and modify the security group to allow all traffic from anywhere

<img width="959" alt="9" src="https://github.com/user-attachments/assets/6886f6fb-c76f-4db4-943b-988899e31ea2" />

9. Connect to the VPC A Private AZ1 server instance using Session Manager and issue the following command:

<img width="372" alt="10 1" src="https://github.com/user-attachments/assets/e2a53a28-b833-4162-a1ff-b366356d19c3" />

10. The previous command created a new S3 bucket, issue the following command to check if we list the contents of the bucket. The bucket is empty so it did not return any listing.

<img width="408" alt="11" src="https://github.com/user-attachments/assets/85864c10-cab6-4ce7-800a-d079281e2a4d" />

11. Issue the following command to create a new file

<img width="232" alt="12" src="https://github.com/user-attachments/assets/72bdb32a-e35b-48da-8b37-1c12d4020171" />

12. Copy the file that was created into the S3 bucket

<img width="535" alt="13" src="https://github.com/user-attachments/assets/6f7ebc85-33eb-4798-8d1a-f7ee9ae04360" />

13. Confirm that the bucket contains the file using the following command

<img width="422" alt="14" src="https://github.com/user-attachments/assets/c64ba4b4-6b92-4ecd-939f-8e944b5a32fd" />

14. Update the VPC Endpoint policy document (policy.json) to remove permissions. This policy removes the s3:Put:* permissions to the VPC Endpoint, effectively preventing instances from VPC A to upload objects to S3 buckets in the account. 

<img width="957" alt="15" src="https://github.com/user-attachments/assets/02fbbdaa-36a4-467e-8532-b5037a3f5281" />

15. Trying to upload the test file again will result will result in an Access denied error. This is because the Endpoint policy allows only Get* and List* actions, effectively making the S3 bucket read only

<img width="941" alt="16" src="https://github.com/user-attachments/assets/ad0fad19-e154-47f6-970d-9fef05d00694" />

16. Clean up resources by deleting the MultiVPC and Prerequisites CloudFormation stacks

## Connecting On-premises

Amazon VPC provides multiple options to integrate existing data center networks with your AWS VPCs, including AWS Managed Site-to-Site (IPsec) VPNs and Direct Connect connections. 

In the hands on lab, I will be doing the following:
* Deploy a VPC containing a simulated data center environment, with DNS server and a simple web application
* Establish VPN connectivity between the simulated data center and the AWS environment
* Set up DNS resolution between the AWS environment and simulated data center
* Test connectivity from the AWS environment to the simulated data center

### Prerequisite steps
* Create a stack on CloudFormation using the prerequisites.yaml CloudFormation template. 

<img width="952" alt="1" src="https://github.com/user-attachments/assets/fd3b9d71-dc3b-4b6f-8cd8-e2d0165354e0" />

* Create a stack on CloudFormation using the multi-vpc-create-all-vpcs-and-tgw.yaml template.

<img width="950" alt="2" src="https://github.com/user-attachments/assets/10fc882c-cc4d-4807-8dfa-ac7a73b8e87d" />

* Create a stack on CloudFormation using the on-premises-create-on-premises.yaml template. This stack will create the following:
 *  VPC that will act as the on-premises environment
 *  A public and private subnet
 *  Three EC2 instances for a Customer Gateway Server, DNS Server and Application Server

I had a problem when I tried to deploy this stack, I hit the quota of the amount of VPCs that I can have in my account. I submitted a quota increase to AWS and my issue was quickly resolved.

<img width="957" alt="3" src="https://github.com/user-attachments/assets/0d9c1ece-ddbf-4b5f-9bdf-277bcaf94e64" />

<img width="956" alt="4" src="https://github.com/user-attachments/assets/dccb2b05-700d-4641-84af-ea0ec061c381" />

1. Create a Transit Gateway VPN attachment

<img width="957" alt="1" src="https://github.com/user-attachments/assets/6c9a5a62-e9b8-4686-99b8-7fc95a4acc73" />

2. Download the configuration file of the VPN connection

<img width="953" alt="4" src="https://github.com/user-attachments/assets/b3728a97-7ac3-4a5a-a577-19c65bda1f74" />

3. Create a new Transit Gateway Route table for the VPN

<img width="952" alt="5" src="https://github.com/user-attachments/assets/d5789c8e-ab7d-441f-94bb-a708ab265a3d" />

4. Associate the VPN attachment to the new Transit Gateway Route table

<img width="957" alt="6" src="https://github.com/user-attachments/assets/ce880bf6-6280-4eeb-bdc2-2bb4c7acea21" />

5. Create propagations for VPC A, VPC B and VPC C

<img width="953" alt="7" src="https://github.com/user-attachments/assets/92cd056a-5915-4d6c-b9f5-0ba718e0fd68" />

<img width="948" alt="8" src="https://github.com/user-attachments/assets/90398a01-969c-4bbc-844a-7b8d8de53518" />

<img width="953" alt="9" src="https://github.com/user-attachments/assets/fab3a25b-99b8-44d6-869b-a6a458a4f3d6" />

6. Update the Transit Gateway Route Tables with the On premises CIDR

<img width="949" alt="10" src="https://github.com/user-attachments/assets/ea4488eb-cd2c-45f6-b6a6-b4c3aae4a8dc" />

<img width="953" alt="11" src="https://github.com/user-attachments/assets/f3878507-f12c-4b23-b79b-94be246c3814" />

7. Update VPC A, VPC B and VPC C Route tables with the On premises CIDR

<img width="954" alt="12" src="https://github.com/user-attachments/assets/911ad1fc-6a09-49db-89ee-8b24130a1f85" />

<img width="952" alt="13" src="https://github.com/user-attachments/assets/99bcd3e3-c135-4568-b96e-cbcf05cc1189" />

<img width="959" alt="14" src="https://github.com/user-attachments/assets/4e150dcf-ba20-4bd5-aec3-223a0f21437f" />

8. Update the customer gateway EC2 instance's security group

<img width="953" alt="15" src="https://github.com/user-attachments/assets/a4cb32a8-5127-4665-9e37-aad66a8d2a37" />

9. Configure OpenSWAN and bring up the tunnel. Now that ww have configured the simulated datacenter VPC and created the VPN connection to the Transit Gateway, we need to configure OpenSWAN on the Customer Gateway and bring up the tunnel

<img width="956" alt="16" src="https://github.com/user-attachments/assets/5f4808ab-9032-41c3-90a2-ebe91df6f5ee" />

10. Connect to the Customer Gateway EC2 Instance using session manager and ping the private IP address of the EC2 instance in the private subnet of VPC A

<img width="479" alt="17" src="https://github.com/user-attachments/assets/ac284d42-dbd4-43b4-aaae-d878f0a5bd14" />

11. On the Customer Gateway instance check which DNS server the host is using

<img width="276" alt="18" src="https://github.com/user-attachments/assets/b90e4ff2-1be0-4d93-921f-99e4841df77b" />

12. Test that the application server is up and running by using the curl command and the hostname, terminate the session when finished

<img width="269" alt="19" src="https://github.com/user-attachments/assets/5e4d410f-905c-4c1a-977a-1582dd3c4c42" />

13. Connect to the VPC A Private AZ! server instance using Session manager and test the connectivity to the on premises application server's using its private IP address

<img width="421" alt="20" src="https://github.com/user-attachments/assets/3564a9d3-1353-4610-86b5-dbe76cde1bdc" />

14. Test the application server using the curl command. The VPN connection is functioning correctly because the command returns "Hello, world" from the application server

<img width="226" alt="21" src="https://github.com/user-attachments/assets/54f4130b-a0ab-432a-87ff-030a775f0763" />

15. Verify that the EC2 instance can reach the on-premises DNS server by querying it directly using the IP address and the dig command

<img width="476" alt="22" src="https://github.com/user-attachments/assets/a1390605-869f-4dce-8c2e-bd389cee4831" />

16. Test the application server by using the curl command and its hostname. This fails because the DNS has not been configured to allow the EC2 instances to resolve to names hosted on the DNS server. Terminate the session when finished.

<img width="340" alt="23" src="https://github.com/user-attachments/assets/926b05f8-30bb-482d-acbb-8f7266b83125" />

17. Configure a Route 53 Resolver Outbound Endpoint. Route 53 Resolver makes hybrid cloud easier for enterprise customers by enabling seamless DNS query resolutions across your entire hybrid cloud.

<img width="955" alt="24" src="https://github.com/user-attachments/assets/1a71b27c-67c0-4ebb-b2e2-9656abc3df6c" />

18. Create a Route 53 Resolver rule for example.corp

<img width="959" alt="25" src="https://github.com/user-attachments/assets/02d681c8-9a0e-4b4f-b837-8a92a75c73ee" />

19. Connect to the VPC B Private AZ1 Server EC2 instance using session manager and check the setting of the DNS server on the instance

<img width="525" alt="26" src="https://github.com/user-attachments/assets/91925cc5-fdac-4e2a-aa4a-773f5e738b0f" />

20. Check that the hostname for myapp.example.corp resolves to an IP address

<img width="254" alt="27" src="https://github.com/user-attachments/assets/1ff052dd-8131-4a42-aae7-6593ecdf9b8b" />

21. Use the curl command to query the on-premises application server by its hostname

<img width="257" alt="28" src="https://github.com/user-attachments/assets/fd4e68b5-0421-420f-8629-1f43605c1707" />

22. Clean up resources

22.1 Delete the Site-to-Site VPN

22.2 Delete the on-premises VPC cloudformation stack

22.3 Delete the Route53 resolver endpoints

22.4 Delete the MultiVPC and Prerequisites CloudFormation stacks

## Network Monitoring 
Amazon CloudWatch is a metrics repository. AWS services send metrics into the repository, and then you retrieve statistics based on those metrics. VPC Flow Logs is a feature that enables you to capture information (meta data) about the IP traffic going to and from network interfaces in your VPC. 

In the hands on lab, I will be doing the following:
* Create a dashboard to view a set of metrics on one page and set up an alarm on a threshold breach
* Set Up VPC Flow logs for VPC A
* Generate some traffic on the EC2 instances in the VPC
* View logs in CloudWatch

### Prerequisite steps
* Create a stack on CloudFormation using the prerequisites.yaml CloudFormation template. 

<img width="952" alt="1" src="https://github.com/user-attachments/assets/fd3b9d71-dc3b-4b6f-8cd8-e2d0165354e0" />

* Create a stack on CloudFormation using the multi-vpc-create-all-vpcs-and-tgw.yaml template.

<img width="950" alt="2" src="https://github.com/user-attachments/assets/10fc882c-cc4d-4807-8dfa-ac7a73b8e87d" />

1. Review automatic CloudWatch dashboards for Nat Gateways

<img width="951" alt="1" src="https://github.com/user-attachments/assets/414d9381-db19-474c-9d16-e5e571d0ebc3" />

2. Create a custom dashboard. The dashboard will have the following:
* A graph of the Network In/Out statistics in bytes for the EC2 instances 
* A widget of the NetworkPacketsOut and NetworkPacketsIn

<img width="959" alt="3" src="https://github.com/user-attachments/assets/4da09f4d-0036-4cdd-b625-8a0840e685b6" />

3. Create a CloudWatch alarm that monitors the amount of traffic received by an EC2 instance

<img width="954" alt="4" src="https://github.com/user-attachments/assets/d04a5a06-9ec4-4b1a-9b7d-6fabc3c673ab" />

4. Create an SNS Topic. Subscribe to the SNS topic to receive an email notification if an alarm threshold is breached.

<img width="687" alt="5" src="https://github.com/user-attachments/assets/7cdea212-48a1-485b-97f7-82b9830ef159" />

<img width="431" alt="6" src="https://github.com/user-attachments/assets/c8c7fdc5-327e-4d2e-b571-7ad4aece5efb" />

5. Create a CloudWatch Log Group

<img width="958" alt="1" src="https://github.com/user-attachments/assets/f5d5e98f-5193-4e27-98ba-f24d298fe28d" />

6. Create a VPC Flow log

<img width="959" alt="2" src="https://github.com/user-attachments/assets/809a12c3-377d-4405-81ed-1b3f7e63c0da" />

7. Connect to the VPC B Private EC2 server using Session Manager and install and run iperf3 server

<img width="952" alt="3" src="https://github.com/user-attachments/assets/e40ec095-9ec7-4d93-9683-353d1d3a5455" />

8. Connect to the VPC A Private EC2 server using Session Manager. Install iperf and set up a TCP transfer with 2 parallel streams for 30 seconds to the EC2 instance in VPC B. When iperf is completed, terminate the Session manager session. Terminate the session for the other instance as well. 

<img width="689" alt="4" src="https://github.com/user-attachments/assets/183bc197-caae-401d-b97f-065c1fe58689" />

9. View the VPC Flow logs for the EC2 Instance in VPC A

<img width="950" alt="5" src="https://github.com/user-attachments/assets/d358211a-fdc6-4455-97a7-71ec966c16f5" />

10. Query the VPC Flow Logs using CloudWatch Logs Insights. Here we are querying the top 10 byte transfers by source and destination IP addresses

<img width="956" alt="6" src="https://github.com/user-attachments/assets/8ffc208b-a766-4746-8bda-80b1f5dfc5a8" />

11. Generating traffic to the Instance in VPC B triggered the CloudWatch. Here is the email that we received from the SNS topic notifying us about the alarm breach.

<img width="712" alt="7" src="https://github.com/user-attachments/assets/2ae06d8d-db24-473e-8c95-a135b87ed659" />

12. Clean Up resources

12.1 Delete CloudWatch Alarm

12.2 Delete the FlowLog CloudWatch Log Group

12.3 Delete the CloudWatch Dashboard

12.4 Delete the MultiVPC and Prerequisites CloudFormation stacks

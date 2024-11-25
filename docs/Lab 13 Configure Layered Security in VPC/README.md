# Step-by-Step Guide for Configuring Layered Security in an AWS VPC

## Step 1: Create VPC
1. Go to VPC Service
2. In Left side panel, click on "Your VPC"
3. Click on "Create VPC"
   ![CreateVPCPage](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/CreateVPCPage.png)
4. Fill up the name for VPC 
5. Set IPv4 CIDR as 10.0.0.0/16
   ![VPCNameAndIPv4CIDR](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/VPCNameAndIPv4CIDR.png)
6. Click on "Create VPC"
   ![VPCCreated](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/VPCCreated.png)

## Step 2: Create Subnet
1. In Left Side Panel, click on "Subnets"
2. Click on "Create Subnet"
   ![CreateSubnetPage](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/CreateSubnetPage.png)
3. Select the VPC ID of the VPC created earlier
   ![SubnetVPCID](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/SubnetVPCID.png)
4. Enter the Name for your Subnet
5. Select Availability Zone 
6. Enter IPv4 Subnet CIDR Block as 10.0.0.0/24
   ![SubnetNameAZIPv4SubnetCIDRBock](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/SubnetNameAZIPv4SubnetCIDRBock.png)
7. Click on "Create Subnet"
   ![SubnetCreated](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/SubnetCreated.png)

## Step 3: Create Internet Gateway
1. In Left Side Panel, click on "Internet Gateways"
2. Click on "Create Internet Gateway"
   ![CreateIGWPage](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/CreateIGWPage.png)
3. Enter a Name for Internet Gateway
   ![IGWName](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/IGWName.png)
4. Click on "Create Internet Gateway"
   ![IGWCreated](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/IGWCreated.png)
5. Click on "Attach to VPC"
6. In Available VPCs Section, select the VPC created earlier
   ![IGWAttachToVPC](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/IGWAttachToVPC.png)
7. Click on "Attach Internet Gateway"
   ![IGWAttached](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/IGWAttached.png)

## Step 4: Create Route Table
1. On Left Side Panel, click on "Route Tables"
2. Click on "Create Route Table"
   ![CreateRouteTablePage](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/CreateRouteTablePage.png)
3. Enter the Name for Route Table
4. Select the VPC created earlier
   ![RouteTableNameVPCSelection](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/RouteTableNameVPCSelection.png)
5. Click on "Create Route Table"
   ![RouteTableCreated](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/RouteTableCreated.png)
6. Select the Route Table just created
7. Go to the Subnet Associations Tab
8. Click on "Edit Subnet Associations"
   ![RouteTableEditSubnetAssocations](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/RouteTableEditSubnetAssocations.png)
9. In Available Subnets, select the Subnet created earlier
   ![RouteTableSelectSubnetAssocations](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/RouteTableSelectSubnetAssocations.png)
10. Click on "Save Associations"
    ![RouteTableSubnetAssociationsEdited](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/RouteTableSubnetAssociationsEdited.png)
11. Go to the Routes Tab
12. Click on "Edit Routes"
    ![RouteTableRoutesPage](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/RouteTableRoutesPage.png)
13. Click on "Add Route"
    ![RouteTableAddRoute](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/RouteTableAddRoute.png)
14. Select Destination as 0.0.0.0/0
15. Set Target as Internet Gateway 
16. Select the Internet Gateway created earlier
    ![RouteTableAddedRoute](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/RouteTableAddedRoute.png)
17. Click on "Save Changes"
    ![RouteTableRoutesEdited](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/RouteTableRoutesEdited.png)

## Step 5: Launch EC2 Instance
1. Go to EC2 Service
2. Click on "Launch Instance"
   ![EC2LaunchInstance](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/EC2LaunchInstance.png)
3. Enter Name for EC2 Instance
   ![EC2Name](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/EC2Name.png)
4. Select Windows as AMI
   ![EC2AMIWindows](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/EC2AMIWindows.png)
5. Ensure Instance Type is t3.micro
   ![EC2InstanceType](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/EC2InstanceType.png)
6. Click on "Create Key Pair"
   ![EC2CreateKeyPair](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/EC2CreateKeyPair.png)
7. Enter Name for Key Pair
8. Click on "Create Key Pair"
9. Save the Key Pair at a secure location on your local machine
   ![EC2KPName](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/EC2KPName.png)
10. In Network Settings, click on "Edit"
11. Select the VPC created earlier (Subnet will be automatically selected)
12. Enable Auto-assign Public IP
    ![EC2NetworkSettings1](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/EC2NetworkSettings1.png)
13. Enter name for Security Group
    ![EC2SGName](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/EC2SGName.png)
14. In Inbound Security Group Rule, click on "Add Security Group Rule"
    ![EC2-AddInboundRule](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/EC2-AddInboundRule.png)
15. Select Type as All Traffic
16. Set Source as Anywhere
    ![EC2SGRule2](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/EC2SGRule2.png)
17. Click on "Launch Instance"
18. Wait for the instance to pass the Status Check
    ![EC2InstanceLaunching](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/EC2InstanceLaunching.png)

## Step 6: Connect to EC2 Instance
1. Select the EC2 Instance
2. Click on "Connect"
   ![EC2Connect](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/EC2Connect.png)
3. In RDP Client Section, copy the Public IP and Username
   ![EC2ConnectToInstance](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/EC2ConnectToInstance.png)
4. On your keyboard, press Windows Key and search for RDP
   ![RDPOpen](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/RDPOpen.png)
5. Open RDP and click on "Show Options"
   ![RDPShowOptions](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/RDPShowOptions.png)
6. Paste the Public IP in the Computer field
7. Enter the Username
   ![RDPIPUsername](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/RDPIPUsername.png)
8. Click on "Connect"
9. Go back to EC2 RDS Client Connection Section
10. Click on "Get Password"
    ![EC2GetPassword](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/EC2GetPassword.png)
11. Click on "Upload Private Key File"
    ![EC2RDPUploadKP](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/EC2RDPUploadKP.png)
12. Select the Key Pair File saved on local machine
13. Click on "Decrypt Password"
    ![EC2RDPKPSelected](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/EC2RDPKPSelected.png)
14. Copy the Password
    ![EC2RDPPasswordDecrypted](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/EC2RDPPasswordDecrypted.png)
15. Paste the Password in the RDP Password field
16. Click "OK"
    ![RDPPasswordPaste](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/RDPPasswordPaste.png)
17. Click "Yes" on the RDP popup
    ![RDPPopUpYes](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/RDPPopUpYes.png)
18. RDP Connection will be Successful
    ![RDPConnectionSuccess](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/RDPConnectionSuccess.png)

## Step 7: Create Network ACL (NACL)
1. Go to VPC Service
2. On Left Side Panel, scroll down to Security Section
3. Click on "Network ACLs"
4. Click on "Create Network ACL"
   ![EC2NACL's](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/EC2NACL's.png)
5. Enter Name for NACL
6. Select the VPC created earlier
   ![NACLNameVPCSelection](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/NACLNameVPCSelection.png)
7. Click on "Create Network ACL"
   ![NACLCreated](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/NACLCreated.png)
8. Select the NACL
9. Go to the Subnet Associations Tab
10. Click on "Edit Subnet Associations"
    ![NACLEditSubentAssociations](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/NACLEditSubentAssociations.png)
11. Select the Available Subnet
12. Click on "Save Changes"
    ![NACLEditSubentSelectAval](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/NACLEditSubentSelectAval.png)
13. Subnet Associations for NACL will be Updated
    ![NACLSubnetAssociationsUpdated](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/NACLSubnetAssociationsUpdated.png)

## Step 8: Configure NACL Inbound and Outbound Rules
### Inbound Rules
1. In Inbound Tab, click on "Edit Inbound Rule"
   ![NACLInbound](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/NACLInbound.png)
2. Click on "Add Rule"
3. Add two rules:
   - Rule 1:
     - Rule Number: 100
     - Type: Custom TCP
     - Port Range: 1024-65535
   - Rule 2:
     - Rule Number: 150
     - Type: RDP
4. Click on "Save Changes"
   ![NACLEditInboundRule](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/NACLEditInboundRule.png)

### Outbound Rules
1. Go to Outbound Rule Tab
2. Click on "Edit Outbound Rule"
   ![NACLOutbound](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/NACLOutbound.png)
3. Click on "Add Rule"
4. Add two rules:
   - Rule 1:
     - Rule Number: 100
     - Type: RDP
   - Rule 2:
     - Rule Number: 150
     - Type: Custom TCP
     - Port Range: 1024-65535
5. Click on "Save Changes"
   ![NACLEditOutboundRule](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/NACLEditOutboundRule.png)

## Step 9: Reconnect RDP
1. Go back to RDP
2. Attempt to connect using Public IP, Username, and Password
   ![RDPConnectionSuccess2](/docs/Lab%2013%20Configure%20Layered%20Security%20in%20VPC/img/RDPConnectionSuccess2.png)

**Note**: If all steps are followed correctly, RDP will connect successfully.
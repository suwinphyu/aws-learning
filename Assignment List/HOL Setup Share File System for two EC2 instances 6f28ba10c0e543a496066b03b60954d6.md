# HOL : Setup Share File System for two EC2 instances

![2tierarchi.drawio (1).png](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/2tierarchi.drawio_(1).png)

# Create Security Group

1. Search “security group” 

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled.png)

## Create App Security Group

1. Create security group with valid group name, description and default VPC 

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%201.png)

1. Setup Inbound rules
2. Choose Type as “SSH” and Source as “Anywhere- IPv4”

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%202.png)

1. Create App Security Group with SSH port 

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%203.png)

## Create EFS Security Group

1. Create security group with valid group name, description and default VPC 

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%204.png)

1. Setup Inbound rules and Type as “NFS”
2. Choose Source as “Custom” with security group = aws_we_ec2_sg

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%205.png)

1. Create EFS Security Group

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%206.png)

# Create EFS(Elastic File System)

1. Search “EFS” → Create file system with “Customize” option 

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%207.png)

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%208.png)

1. Setup “File system type” as Regional
2. Enable automatic backups as default
3. In Lifecycle management → Select None in “Transition into Archive-new”
4. Select “Transition into Standard” as On first access 
5. Turn OFF “Enable encryption of data at rest” 

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%209.png)

1. For performance settings, “Enhanced” is suitable for production . Currently, we will use “Bursting” for testing purpose

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%2010.png)

1. Network access → Select default VPC
2. In Mount targets, remove default security first and add aws_we_efs_sg for all availability zone

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%2011.png)

1. For File system policy, use as default settings

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%2012.png)

1. Review and Create file system 

![screencapture-ap-southeast-2-console-aws-amazon-efs-home-2024-03-18-00_10_11.png](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/screencapture-ap-southeast-2-console-aws-amazon-efs-home-2024-03-18-00_10_11.png)

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%2013.png)

# Create EC2(**Elastic Compute Cloud**)

1. Search “EC2” → Create Instance for EC2 server 1

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%2014.png)

1. Choose Amazon Linux 2 AMI(HVM) and 64 bit (x86) Architecture

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%2015.png)

1. Select t2.micro for Instance type 
2. Select key pair 

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%2016.png)

1. Network settings → Edit → Select default VPC
2. Select subnet as ap_southeast_2a zone for EC2 Server 1
3. Select existing security group → choose aws_we_ec2_sg

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%2017.png)

1. Configure storage → Edit “0 x File systems”

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%2018.png)

1. File systems → there are 2 file systems : FSx (for window instance) and EPS (for linux instance) → Choose EPS instance 
2. Add shared file system → select aws_we_shared_file and mount point
3. Check OFF “Automatically create and attach security groups” option because we have already created security groups in above

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%2019.png)

1. Launch instance 

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%2020.png)

1. Create another instance for EC2 server 2

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%2021.png)

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%2022.png)

1. Select subnet as ap_southest_2b for EC2 server 2
2. Select existing security group as aws_we_ec2_sg used for same one both both EC2 servers

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%2023.png)

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%2024.png)

1. Launch EC2 server 2

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%2025.png)

# Connect to instance

1. Connect to instance EC2 server1 from browser 

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%2026.png)

1. Enter “df -h” in console and check mount = /mnt/efs/we as result 

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%2027.png)

1. Create newfile.txt on Server 1

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%2028.png)

1. Connect to instance EC2 server2 from browser 

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%2029.png)

1. newfile.txt uploaded from Server 1 is able to access from Server 2 

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%2030.png)

1. Update newfile.txt from Server2

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%2031.png)

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%2032.png)

1. Server1 is able to access the update file from Server2

![Untitled](HOL%20Setup%20Share%20File%20System%20for%20two%20EC2%20instances%206f28ba10c0e543a496066b03b60954d6/Untitled%2033.png)
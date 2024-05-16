# Assignment: RDS Lab

## Create Security Groups for EC2

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled.png)

1. Create security group with valid group name, description and default VPC 
2. Setup Inbound rules ->Choose Type as “SSH” and Source as “Anywhere- IPv4”

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%201.png)

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%202.png)

## Create Security Groups for RDS (relational database system)

1. Create security group with valid group name, description and default VPC 
2. Setup Inbound rules and Type as "MySQL"
3. Choose Source as “Custom” with security group used for EC2

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%203.png)

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%204.png)

# Create RDS

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%205.png)

1. Create Database → Standard Create 

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%206.png)

1. Select MySQL and Engine version 8.0.35

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%207.png)

1. Select “Single DB instance” with Dev/Test template

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%208.png)

1. Setup credentials 

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%209.png)

1. Choose “Burstable classes” with t3.micro

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2010.png)

1. Setup Storage with 50GB 

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2011.png)

1. Manually setup connection with EC2

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2012.png)

1. Select Security group

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2013.png)

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2014.png)

1. Setup authentication 

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2015.png)

1. Setup Backup 

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2016.png)

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2017.png)

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2018.png)

1. Review cost summary

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2019.png)

# Create EC2

1. Search “EC2” →  Launch Instance  

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2020.png)

1. Select “Ubuntu” with default image 

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2021.png)

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2022.png)

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2023.png)

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2024.png)

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2025.png)

# Connect to instance

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2026.png)

type “htop”

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2027.png)

type “sudo apt update”

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2028.png)

type “sudo apt install mysql-client-core-8.0”

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2029.png)

## Command for connect MySQL

Host: -h (host name or IP)
Port -P (network port -3306)
User: -u (user name)
Password: -p

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2030.png)

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2031.png)

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2032.png)

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2033.png)

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2034.png)

CREATE DATABASE devktops;
SHOW DATABASES;
GRANT ALL PRIVILEGES ON devktops.* TO 'localuser'@'localhost' WITH GRANT OPTION;
FLUSH PRIVILEGES;

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2035.png)

USE devktops;
CREATE TABLE courses (
course_id int NOT NULL,
course_name varchar(250) NOT NULL,
instructor_name varchar(250) NOT NULL,
topic varchar(50) NOT NULL,
PRIMARY KEY (course_id)
);
DESCRIBE courses;
SHOW COLUMNS FROM courses;

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2036.png)

## Modify Database settings

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2037.png)

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2038.png)

## Create Replica

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2039.png)

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2040.png)

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2041.png)

## Create DB Snapshot

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2042.png)

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2043.png)

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2044.png)

## Disable Delete Protection

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2045.png)

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2046.png)

## Delete Primary Database

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2047.png)

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2048.png)

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2049.png)

## Replica becomes primary instance

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2050.png)

## Delete Replica

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2051.png)

## Delete Snapshot

![Untitled](Assignment%20RDS%20Lab%202d579ca49ea34ab4b614c208db31a27f/Untitled%2052.png)
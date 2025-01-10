Step 1: Launch an EC2 Instance
1. Login to AWS Console: Go to AWS Management Console, log in, and
navigate to the EC2 service.
2. Launch an Instance:
○ Choose an Amazon Machine Image (AMI), such as Amazon
Linux 2 or Ubuntu.
○ Choose an instance type (e.g., t2.micro for free tier).
○ Configure instance details, security group, and storage.
○ Set up the Security Group to allow HTTP (port 80), HTTPS (port
443), and SSH (port 22) access.
○ Launch the Instance and keep the private as default

Step 2: Connect to EC2 instance
1. Connect via SSH: Open a terminal and run the following command
and update the packages by using command in terminal :
sudo yum update -y # For Amazon Linux
sudo apt update -y # For Ubuntu
2. Install Nginx

Step 3 : Start and Enable Nginx by using these commands in
terminal

Step 4 : Upload application code file if you want otherwise the
default index.html page that is distributed with nginx on Amazon
Linux. It is located in /usr/share/nginx/html.

- now put your content in a location of your choice and edit the root configuration
directive in the nginx configuration file /etc/nginx/nginx.conf.

Step 5 : Test & Check the web-page using public IP address and
port number
- http://<public IP>:<port>

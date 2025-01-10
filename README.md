#PROJECT-1 :- Hosting a website on AWS EC2 instance
by using the NGINX web server.

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

#PROJECT-2 :- Creating & Hosting an static website using
AWS S3 service

Step 1: Create an S3 Bucket
1. Log in to AWS Management Console: Go to AWS Console.
2. Navigate to S3: Search for "S3" in the AWS search bar and select the S3 service.
3. Click "Create Bucket":
○ Enter a unique bucket name (e.g., my-static-website).
○ Choose the appropriate AWS region.
4. Configure Bucket Options:
○ Uncheck the "Block all public access" option & save changes.
○ Confirm the warning and allow public access.
5. Create the Bucket: Click the "Create bucket" button.

Step 2: Upload Website Files
1. Open Your Bucket: Click on the bucket you just created.
2. Upload Files:
○ Click "Upload" and select your website files (e.g., index.html and error.html).
○ Ensure you include all necessary files (e.g., CSS, JS, images, etc.).
3. Set Permissions:
○ Under the permissions tab during upload, ensure files are publicly accessible.

Step 3: Enable Static Website Hosting
1. Go to Properties: In the bucket dashboard, select the "Properties" tab.
2. Enable Static Website Hosting:
○ Scroll to the "Static Website Hosting" section.
○ Click "Edit" and enable the option.
○ Specify:
■ Index document: index.html
■ Error document: error.html (optional)
○ Save your changes
3. Copy the Endpoint URL: Note the provided bucket website endpoint URL. This is your
website URL.

Step 4: Set Permissions for Public Access
1. Add a Bucket Policy:
○ Go to the "Permissions" tab and select "Bucket Policy".
Paste the following policy (replace BUCKET_NAME with your bucket's name):
json
○ Save the policy.

Step 5: Test Your Website
1. Open the S3 Bucket Endpoint URL in your browser.
2. ○ Save the policy.

#PROJECT-3 :- Implementing Setting Up Auto Scaling in AWS
Step 1: Launch an EC2 Instance
1. Log in to AWS Console: Navigate to the AWS Management Console.
2. Go to EC2: From the services menu, select EC2.
3. Launch an EC2 Instance:
○ Choose an Amazon Machine Image (AMI) and instance type.
○ Congure network settings and security groups.
○ Install necessary applications or scripts for the instance.
4. Create a Key Pair: Download it for SSH access to the instance.
5. Once launched, ensure the instance is accessible and functioning.

Step 2: Create a Launch Template or Launch Conguration
1. Go to Launch Templates:
○ From the EC2 dashboard, select Launch Templates.
○ Click Create Launch Template.
2. Fill Template Details:
○ Provide a name and description.
○ Specify the AMI, instance type, and key pair.
○ Congure storage, network, and security settings.
○ Add any startup scripts in the User Data section.
3. Save the Launch Template.
Alternatively, you can create a Launch Conguration:
● Navigate to the Auto Scaling section and select Launch Congurations.
● Follow similar steps to dene instance settings.

Step 3: Create an Auto Scaling Group
1. Navigate to Auto Scaling Groups:
○ From the EC2 dashboard, select Auto Scaling Groups.
2. Create a New Auto Scaling Group:
○ Choose the Launch Template or Launch Conguration created earlier.
3. Congure Group Details:
○ Specify the VPC and subnets where instances will be launched.
○ Set the minimum, maximum, and desired number of instances.
4. Attach Load Balancer (Optional):
○ Attach an existing Application Load Balancer or Classic Load Balancer to
distribute trafc.
5. Set Scaling Policies:
○ Enable scaling based on metrics like CPU Utilization or custom CloudWatch
alarms.
○ Example: Add instances if CPU > 70% and remove instances if CPU < 20%.
6. Review and Create:
○ Conrm the settings and create the Auto Scaling Group.

Step 4: Congure Scaling Policies
1. Dynamic Scaling:
○ Navigate to the Auto Scaling Group settings.
○ Add policies to scale in or out based on CloudWatch alarms.
○ Example:
■ Scale Out: Add instances when CPU exceeds 70%.
■ Scale In: Remove instances when CPU drops below 20%.
2. I have chosen dynamic scaling , but you can choose Predictive scaling policies or
Scheduled actions as per your choice.

Step 5: Test the Auto Scaling
1. Simulate Load:
○ Use tools like stress to increase CPU usage or generate trafc.
- To increase CPU stress for testing purposes on an AWS EC2 instance via SSH,
you can use the stress tool. Here's how you can do it:
- Steps to Stress Test the CPU:
- Install Stress Tool (if not already installed):
2. Run Stress Command:
Example to stress the CPU with 5 workers for 60 seconds:
3. Check CPU Usage (Optional):
Use the top or htop command in another terminal session to monitor the CPU usage:
top
4. Stop Stress Test:
If you want to stop the stress test before it completes, press Ctrl+C in the terminal running the
stress command.
5. Monitor Scaling Activity:
○ Go to the Activity tab in the Auto Scaling Group to track instance launches and
terminations.

#PROJECT-4 :- Setting Up a Elastic Load Balancer (ELB) - Classic Load Balancer (CLB)

Step 1: Launch EC2 Instances
1. Log in to AWS Console: Navigate to AWS Management Console.
2. Navigate to EC2: From the Services menu, choose EC2.
3. Launch EC2 Instances:
○ Create at least two EC2 instances.
○ Ensure the instances are in the same VPC.
○ Install a web server (e.g., Apache, Nginx) and set up a basic webpage.

Step 2: Configure a Security Group
1. Create or Update a Security Group for EC2 Instances:
○ Allow inbound HTTP traffic on port 80.
○ Allow traffic from the Load Balancer’s security group.
2. Ensure the Security Group for the Load Balancer allows inbound HTTP traffic
from all sources (0.0.0.0/0).

Step 3: Create a Classic Load Balancer
1. Go to the EC2 Dashboard: Under Load Balancing, click Load Balancers.
2. Click "Create Load Balancer":
○ Choose Classic Load Balancer.
3. Basic Configuration:
○ Provide a name for the load balancer.
○ Select the VPC where your EC2 instances are located.
○ Listeners: Add HTTP on port 80 (or HTTPS on port 443 if needed).
4. Subnets: Choose at least two subnets in different availability zones for high
availability.

Step 4: Configure Health Checks
1. Set Health Check Parameters:
○ Protocol: HTTP.
○ Ping Path: / (or specify a custom health check path).
○ Response Timeout: 5 seconds.
○ Interval: 30 seconds.
○ Healthy/Unhealthy Threshold: Set the number of successful or failed
checks required to mark an instance healthy or unhealthy.
2. Save the Health Check configuration.

Step 5: Register EC2 Instances
1. Select Instances:
○ Choose the EC2 instances you launched earlier.
2. Add Instances to the load balancer.
3. Review and confirm the registration.

Step 6: Configure Security Settings (Optional for HTTPS)
1. Enable HTTPS:
○ Use AWS Certificate Manager (ACM) to get an SSL certificate.
○ Add an HTTPS listener and attach the SSL certificate.
2. Update Security Group:
○ Allow inbound traffic on port 443 for HTTPS.

Step 7: Test the Load Balancer
1. Get the DNS Name:
○ Go to the CLB details page and copy the DNS name.
2. Test in a Browser:
○ Paste the DNS name into a browser to ensure traffic is distributed
between the instances.
3. As we refresh the browser we can observe that traffic is distributed between the
instances.

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


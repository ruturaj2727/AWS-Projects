# AWS Project Suite

## Table of Contents
1. [Hosting a Website on AWS EC2 Instance Using NGINX](#project-1-hosting-a-website-on-aws-ec2-instance-using-nginx)
2. [Creating & Hosting a Static Website Using AWS S3](#project-2-creating-hosting-a-static-website-using-aws-s3)
3. [Implementing Auto Scaling in AWS](#project-3-implementing-auto-scaling-in-aws)
4. [Setting Up Elastic Load Balancer (ELB)](#project-4-setting-up-elastic-load-balancer-elb)

---

## Project 1: Hosting a Website on AWS EC2 Instance Using NGINX

### Steps:

1. **Launch an EC2 Instance**
    - Login to AWS Console and navigate to the EC2 service.
    - Choose an Amazon Machine Image (AMI) such as Amazon Linux 2 or Ubuntu.
    - Select an instance type (e.g., `t2.micro` for free tier).
    - Configure security group:
        - Allow HTTP (port 80), HTTPS (port 443), and SSH (port 22).
    - Launch the instance.

2. **Connect to EC2 Instance**
    - Use SSH to connect:
      ```bash
      ssh -i <your-key.pem> ec2-user@<public-ip>
      ```
    - Update packages:
      ```bash
      sudo yum update -y   # For Amazon Linux
      sudo apt update -y   # For Ubuntu
      ```

3. **Install and Configure NGINX**
    - Install NGINX:
      ```bash
      sudo yum install nginx -y   # For Amazon Linux
      sudo apt install nginx -y   # For Ubuntu
      ```
    - Start and enable NGINX:
      ```bash
      sudo systemctl start nginx
      sudo systemctl enable nginx
      ```

4. **Upload Application Code**
    - Default `index.html` location: `/usr/share/nginx/html`.
    - Modify NGINX configuration in `/etc/nginx/nginx.conf` if needed.

5. **Access the Website**
    - Use the public IP of the instance in your browser:
      ```
      http://<public-ip>
      ```

---

## Project 2: Creating & Hosting a Static Website Using AWS S3

### Steps:

1. **Create an S3 Bucket**
    - Log in to AWS Console and navigate to S3.
    - Click "Create Bucket" and configure:
      - Provide a unique bucket name (e.g., `my-static-website`).
      - Choose the region and disable "Block all public access".

2. **Upload Website Files**
    - Open the bucket and upload files (e.g., `index.html`, `error.html`).
    - Ensure files are publicly accessible by modifying permissions.

3. **Enable Static Website Hosting**
    - Go to the "Properties" tab and enable static website hosting.
    - Specify:
      - Index document: `index.html`
      - Error document: `error.html` (optional)

4. **Set Bucket Policy**
    - Add the following policy:
      ```json
      {
        "Version": "2012-10-17",
        "Statement": [
          {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::<BUCKET_NAME>/*"
          }
        ]
      }
      ```
    - Replace `<BUCKET_NAME>` with your bucket's name.

5. **Test the Website**
    - Open the S3 bucket endpoint URL in your browser.

---

## Project 3: Implementing Auto Scaling in AWS

### Steps:

1. **Launch an EC2 Instance**
    - Navigate to EC2 and launch an instance.
    - Configure security group and ensure the instance is functioning.

2. **Create a Launch Template**
    - Go to "Launch Templates" and create a template with:
      - AMI, instance type, key pair, storage, and security settings.
      - Add startup scripts in the "User Data" section if needed.

3. **Create an Auto Scaling Group**
    - Specify the launch template and configure:
      - VPC and subnets.
      - Minimum, maximum, and desired number of instances.
      - Optional: Attach a load balancer.
    - Define scaling policies:
      - Example: Add instances if CPU > 70%, remove if CPU < 20%.

4. **Test Auto Scaling**
    - Simulate load using tools like `stress`:
      ```bash
      sudo apt install stress -y
      stress --cpu 5 --timeout 60
      ```
    - Monitor scaling activity in the "Activity" tab of the Auto Scaling Group.

---

## Project 4: Setting Up Elastic Load Balancer (ELB)

### Steps:

1. **Launch EC2 Instances**
    - Create at least two EC2 instances in the same VPC.
    - Install a web server and set up basic webpages.

2. **Configure Security Groups**
    - Allow HTTP traffic on port 80 and traffic from the Load Balancer's security group.

3. **Create a Classic Load Balancer (CLB)**
    - Go to EC2 dashboard and create a CLB.
    - Configure listeners (HTTP/HTTPS) and subnets in multiple availability zones.

4. **Configure Health Checks**
    - Set parameters such as:
      - Ping path: `/`
      - Interval: 30 seconds
      - Healthy threshold: 3

5. **Register Instances**
    - Attach EC2 instances to the CLB.

6. **Test the Load Balancer**
    - Use the CLB DNS name to test in a browser.
    - Verify traffic distribution across instances.

---

### Notes
- Ensure you follow AWS best practices for security and scalability.
- Test thoroughly to verify configurations.

---

### Author
This project suite is authored and maintained by RUTURAJ SONONE. Feel free to contribute or report issues via GitHub.

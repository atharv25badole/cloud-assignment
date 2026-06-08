# Cloud Assignment Documentation

## Project Overview

This project demonstrates how to:

* Launch an AWS EC2 instance
* Install and configure Nginx
* Host a static profile website
* Configure Elastic IP
* Containerize the website using Docker
* Organize project structure
* Push code to GitHub

---

# Project Structure

```bash
cloud-assignment/
│
├── terraform/
├── docker/
└── monolith/
```

---

# 1. AWS EC2 Setup

## Step 1: Launch EC2 Instance

1. Login to AWS Console
2. Go to EC2 Dashboard
3. Click "Launch Instance"
4. Select Ubuntu Server
5. Choose instance type: `t2.micro`
6. Create or select key pair
7. Allow:

   * SSH (22)
   * HTTP (80)
8. Launch instance

---

## Step 2: Connect to EC2

```bash
ssh -i your-key.pem ubuntu@your-public-ip
```

Example:

```bash
ssh -i ubuntu_key.pem ubuntu@13.xx.xx.xx
```

---

# 2. Install Nginx

## Update packages

```bash
sudo apt update
```

## Install Nginx

```bash
sudo apt install nginx -y
```

## Start Nginx

```bash
sudo systemctl start nginx
```

## Enable Nginx

```bash
sudo systemctl enable nginx
```

## Verify Nginx

```bash
sudo systemctl status nginx
```

---

# 3. Host Static Website

## Navigate to web root

```bash
cd /var/www/html
```

## Remove default page

```bash
sudo rm index.nginx-debian.html
```

## Create website

```bash
sudo nano index.html
```

## Sample HTML

```<!DOCTYPE html>
<html>
<head>
    <title>My Profile</title>
    <style>
        body {
            background: #0f172a;
            color: white;
            text-align: center;
            font-family: Arial;
        }
        .card {
            margin-top: 100px;
        }
        img {
            border-radius: 50%;
        }
    </style>
</head>
<body>
    <div class="card">
        <img src="https://via.placeholder.com/150" alt="profile">
        <h1>Hello, I'm Atharv</h1>
        <p>Aspiring Developer | Learning DevOps</p>
        <p>Hosted on AWS EC2 using Nginx with docker</p>
        <a href="https://github.com/">My GitHub</a>
    </div>
</body>
</html>
```

## Reload Nginx

```bash
sudo systemctl reload nginx
```

## Access website

```bash
http://your-public-ip
```

---

# 4. Configure Elastic IP

## Steps

1. Open EC2 Dashboard
2. Go to Elastic IPs
3. Allocate Elastic IP
4. Associate Elastic IP with EC2 instance

## Verify

```bash
http://your-elastic-ip
```

---

# 5. Docker Installation

## Install Docker

```bash
sudo apt install docker.io -y
```

## Start Docker

```bash
sudo systemctl start docker
```

## Enable Docker

```bash
sudo systemctl enable docker
```

## Verify Docker

```bash
docker --version
```

---

# 6. Dockerize Website

## Create project folder

```bash
mkdir mysite
cd mysite
```

## Create HTML file

```bash
nano index.html
```

## Run Nginx container

```bash
sudo docker run -d -p 80:80 \
-v /home/ubuntu/mysite:/usr/share/nginx/html \
--name my-nginx nginx
```

## Verify container

```bash
sudo docker ps
```

## Restart container

```bash
sudo docker restart my-nginx
```

## Stop container

```bash
sudo docker stop my-nginx
```

## Remove container

```bash
sudo docker rm -f my-nginx
```

---

# 7. Terraform Setup

## Create terraform folder

```bash
mkdir terraform
cd terraform
```

## Create main.tf

```bash
nano main.tf
```

## Sample Terraform Code

```hcl
provider "aws" {
  region = "ap-south-1"
}

resource "aws_instance" "web" {
  ami           = "ami-0f5ee92e2d63afc18"
  instance_type = "t2.micro"

  tags = {
    Name = "nginx-server"
  }
}
```

## Initialize Terraform

```bash
terraform init
```

## Validate configuration

```bash
terraform validate
```

## Plan deployment

```bash
terraform plan
```

## Apply configuration

```bash
terraform apply
```

---

# 8. Git and GitHub Commands

## Initialize Git

```bash
git init
```

## Add files

```bash
git add .
```

## Commit files

```bash
git commit -m "Initial commit"
```

## Rename branch

```bash
git branch -M main
```

## Add remote repository

```bash
git remote add origin https://github.com/your-username/cloud-assignment.git
```

## Push to GitHub

```bash
git push -u origin main
```

---

# 9. Useful Docker Commands

## View running containers

```bash
docker ps
```

## View all containers

```bash
docker ps -a
```

## Pull image

```bash
docker pull nginx
```

## View images

```bash
docker images
```

## Remove image

```bash
docker rmi image-name
```

## Access container terminal

```bash
docker exec -it my-nginx bash
```

---

# 10. Final Outcome

Successfully completed:

* AWS EC2 setup
* Nginx installation
* Static website hosting
* Elastic IP configuration
* Docker container deployment
* Terraform configuration
* GitHub repository management

GitHub Repository:
https://github.com/atharv25badole/cloud-assignment

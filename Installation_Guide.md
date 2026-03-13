# 🚀 CloudDeploy - Docker Deployment on AWS EC2

This project demonstrates how to deploy an application using **Docker on AWS EC2** and push the Docker image to **Docker Hub and AWS ECR**.

🔗 **Project Repository**
https://github.com/juhisinha422/clouddeploy

---

# 🖥️ Infrastructure Used

* AWS EC2 Instance
* Amazon Linux
* Instance Type: **t3.micro**
* Docker
* Git
* AWS CLI
* Docker Hub
* AWS ECR

---

# ⚙️ Server Setup

## Update the Server

```
sudo yum update -y
```

## Install Git

```
sudo yum install git -y
git --version
```

---

# 🐳 Install Docker

Install Docker

```
sudo yum install docker -y
```

Start Docker

```
sudo systemctl start docker
```

Enable Docker

```
sudo systemctl enable docker
```

Give permission to ec2-user

```
sudo usermod -aG docker ec2-user
```

Reload shell

```
newgrp docker
```

Check Docker

```
docker --version
```

---

# ☁️ Install AWS CLI

Download AWS CLI

```
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
```

Install unzip

```
sudo yum install unzip -y
```

Unzip

```
unzip awscliv2.zip
```

Install AWS CLI

```
sudo ./aws/install
```

Check AWS CLI

```
aws --version
```

---

# 🔐 Configure AWS CLI

```
aws configure
```

Enter

```
AWS Access Key
AWS Secret Access Key
Region (example: us-east-1)
Output format: json
```

---

# 🔧 Install Docker Build Tools

```
sudo yum install -y gcc make
```

---

# 📂 Clone the Project

```
git clone https://github.com/juhisinha422/clouddeploy.git
```

Go inside project

```
cd clouddeploy
```

Check files

```
ls
```

---

# 🐳 Build Docker Image

```
docker build -t clouddeploy-app .
```

Check images

```
docker images
```

---

# ▶️ Run Docker Container

```
docker run -d -p 3000:3000 clouddeploy-app
```

Check running containers

```
docker ps
```

Test application

```
curl localhost:3000
```

Check port

```
sudo netstat -tulpn | grep 3000
```

---

# 🐳 Push Docker Image to Docker Hub

Login to Docker Hub

```
docker login
```

Enter

```
Username: juhisinha
Password: <DockerHub password or access token>
```

Tag image

```
docker tag clouddeploy-app juhisinha/clouddeploy-app:latest
```

Check images

```
docker images
```

Push image

```
docker push juhisinha/clouddeploy-app:latest
```

Docker Hub Repository

https://hub.docker.com/r/juhisinha/clouddeploy-app

---

# ☁️ Push Docker Image to AWS ECR

## Create ECR Repository

```
aws ecr create-repository \
--repository-name clouddeploy \
--region us-east-1
```

---

## Login to AWS ECR

```
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin ACCOUNT_ID.dkr.ecr.us-east-1.amazonaws.com
```

Replace **ACCOUNT_ID** with your AWS Account ID.

---

## Tag Docker Image for ECR

```
docker tag clouddeploy-app ACCOUNT_ID.dkr.ecr.us-east-1.amazonaws.com/clouddeploy:latest
```

---

## Push Image to ECR

```
docker push ACCOUNT_ID.dkr.ecr.us-east-1.amazonaws.com/clouddeploy:latest
```

---

# ▶️ Run Container from ECR Image

```
docker run -d -p 3000:3000 ACCOUNT_ID.dkr.ecr.us-east-1.amazonaws.com/clouddeploy:latest
```

---

# 🌐 Access the Application

Open browser

```
http://EC2_PUBLIC_IP:3000
```

Example

```
http://13.xx.xx.xx:3000
```

---

# 📚 Learning Outcomes

Through this project you learn

* AWS EC2 setup
* Docker installation and configuration
* Building Docker images
* Running Docker containers
* Pushing images to Docker Hub
* Using AWS ECR
* Basic DevOps deployment workflow

---

# 👩‍💻 Author

**Juhi Sinha**
DevOps Enthusiast | AWS | Docker | CI/CD


# Flask + Express AWS Deployment Project

This project demonstrates multiple deployment strategies for a full-stack application using Flask backend, Express/React frontend, Docker, and AWS cloud services.

---

# 🚀 Technologies Used

- Python Flask
- Node.js / Express
- React
- MongoDB Atlas
- Docker
- Nginx
- PM2
- Gunicorn
- AWS EC2
- AWS ECS Fargate
- AWS ECR
- AWS VPC
- AWS ALB

---

# 📌 Project Deployment Scenarios

# 1️⃣ Single EC2 Deployment

Deployed both Flask backend and Express frontend on a single Ubuntu EC2 instance.

## Features

- Flask backend running on Port 5000
- Express frontend running on Port 3000
- Nginx configured as reverse proxy
- PM2 used for process management
- Gunicorn used for Flask production deployment
- Single Public IP access
- Security groups configured for:
  - SSH (22)
  - HTTP (80)

---

## Architecture

```text
Browser → Nginx → Frontend (3000)
                     ↓
                 Backend (5000)
                     ↓
                MongoDB Atlas
```

---

## Important Commands

### Clone Repository

```bash
git clone <repo-url>
```

### Frontend Setup

```bash
cd frontend
npm install
pm2 start server.js --name frontend
```

### Backend Setup

```bash
cd backend
pip install -r requirements.txt
gunicorn --bind 0.0.0.0:5000 app:app
```

### Restart Services

```bash
pm2 restart frontend
sudo systemctl restart nginx
```

---

# 2️⃣ Separate EC2 Deployment

Frontend and backend deployed on separate AWS EC2 instances.

---

## Architecture

```text
Browser
   ↓
Frontend EC2 (Node/Express)
   ↓
Backend EC2 (Flask + Gunicorn)
   ↓
MongoDB Atlas
```

---

## Features

- Frontend hosted on EC2 Instance #1
- Backend hosted on EC2 Instance #2
- Axios used for frontend-backend communication
- Nginx reverse proxy configured
- PM2 process manager enabled
- Gunicorn for Flask deployment

---

## Important Commands

### Frontend

```bash
pm2 start server.js --name frontend
pm2 restart frontend
pm2 logs frontend
```

### Backend

```bash
gunicorn --bind 0.0.0.0:5000 app:app
sudo ss -tulpn | grep 5000
```

### Test Backend

```bash
curl http://BACKEND_PUBLIC_IP:5000
```

### Restart Nginx

```bash
sudo nginx -t
sudo systemctl restart nginx
```

---

## Important Concept

- Browser communicates only with frontend
- Frontend communicates with backend API
- Backend returns data to frontend
- Frontend sends final response to browser

---

# 3️⃣ Dockerized Deployment using AWS ECS + ECR + VPC

Containerized deployment using Docker and AWS cloud-native services.

---

## Architecture

```text
Internet
   ↓
Application Load Balancer (ALB)
   ↓
Frontend ECS Service (React/Express)
   ↓
Backend ECS Service (Flask API)
   ↓
MongoDB Atlas
```

---

# ☁️ AWS Services Used

- AWS EC2
- AWS ECR
- AWS ECS Fargate
- AWS VPC
- AWS Application Load Balancer

---

# 📦 ECS Deployment Steps

1. Install Docker, AWS CLI, and Git

2. Configure AWS CLI using:

```bash
aws configure
```

3. Create Dockerfile for Flask Backend

4. Create Dockerfile for Express/React Frontend

5. Build Backend Docker Image

6. Build Frontend Docker Image

7. Create Backend ECR Repository

8. Create Frontend ECR Repository

9. Login Docker to ECR

```bash
aws ecr get-login-password --region eu-north-1 | docker login --username AWS --password-stdin ACCOUNT_ID.dkr.ecr.eu-north-1.amazonaws.com
```

10. Tag Docker Images

11. Push Docker Images to ECR

12. Create AWS VPC with Public Subnets

13. Create ECS Cluster using Fargate

14. Create Security Groups

15. Create Backend Task Definition

16. Create Frontend Task Definition

17. Create Application Load Balancer

18. Create Target Groups

19. Configure ALB Listener Rules

20. Create ECS Services

21. Verify ECS Tasks

22. Open ALB DNS URL

23. Test Backend API

24. Push Code to GitHub

25. Stop ECS Services after submission to reduce AWS cost

---

# 🐳 Docker Commands

## Build Images

### Backend

```bash
docker build -t backend .
```

### Frontend

```bash
docker build -t frontend .
```

---

## Tag Images

### Backend

```bash
docker tag backend ACCOUNT_ID.dkr.ecr.eu-north-1.amazonaws.com/backend:latest
```

### Frontend

```bash
docker tag frontend ACCOUNT_ID.dkr.ecr.eu-north-1.amazonaws.com/frontend:latest
```

---

## Push Images

### Backend

```bash
docker push ACCOUNT_ID.dkr.ecr.eu-north-1.amazonaws.com/backend:latest
```

### Frontend

```bash
docker push ACCOUNT_ID.dkr.ecr.eu-north-1.amazonaws.com/frontend:latest
```

---

# 🔐 Security Group Configuration

## Allow

- SSH → Port 22
- HTTP → Port 80
- Backend → Port 5000
- Frontend → Port 3000

---

# 📁 Project Structure

```text
project/
│
├── backend/
│   ├── app.py
│   ├── requirements.txt
│   └── Dockerfile
│
├── frontend/
│   ├── package.json
│   ├── src/
│   └── Dockerfile
│
└── README.md
```

---

# 🌐 Deployment URLs

## Frontend

```text
http://FRONTEND_PUBLIC_IP
```

## Backend

```text
http://BACKEND_PUBLIC_IP:5000
```

## ECS ALB URL

```text
http://ALB-DNS
```

---

# 📚 Key Learning Outcomes

- EC2 instance management
- Nginx reverse proxy setup
- Docker containerization
- ECS Fargate deployment
- ECR image management
- Application Load Balancer setup
- AWS VPC networking
- Production deployment architecture
- PM2 process management
- Flask deployment using Gunicorn

---

# 👨‍💻 Author

Rushikesh Dhule

---

# ⭐ GitHub Repository

If you found this project useful, give it a star ⭐

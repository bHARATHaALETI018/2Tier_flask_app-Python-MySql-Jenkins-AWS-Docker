# 🚀 Bharath's DevSpace - 2-Tier Flask Web Application

> A modern, containerized Flask web application with MySQL database, featuring automated CI/CD deployment on AWS EC2.

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://python.org)
[![Docker](https://img.shields.io/badge/Docker-Ready-blue.svg)](https://docker.com)
[![AWS](https://img.shields.io/badge/AWS-EC2-orange.svg)](https://aws.amazon.com/ec2/)
[![Jenkins](https://img.shields.io/badge/Jenkins-CI%2FCD-red.svg)](https://jenkins.io/)

## 📖 About This Project

Welcome to **Bharath's DevSpace**! This is a showcase project demonstrating modern DevOps practices through a beautiful, responsive 2-tier web application. The app features a sleek glassmorphism design with animated backgrounds and serves as both a personal portfolio and a messaging platform.

### ✨ What Makes This Special?

- **🎨 Modern UI/UX**: Beautiful glassmorphism design with animated gradient backgrounds
- **📱 Fully Responsive**: Works perfectly on desktop, tablet, and mobile devices
- **🐳 Containerized**: Complete Docker setup with multi-container orchestration
- **☁️ Cloud-Native**: Deployed on AWS EC2 with production-ready configuration
- **🔄 CI/CD Pipeline**: Automated deployment using Jenkins for seamless updates
- **💾 Persistent Data**: MySQL database with proper volume management

## 🏗️ Architecture Overview

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Frontend      │    │   Backend       │    │   Database      │
│   (HTML/CSS/JS) │◄──►│   (Flask App)   │◄──►│   (MySQL)       │
│                 │    │   Port: 5000    │    │   Port: 3306    │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         └───────────────────────┼───────────────────────┘
                                 │
                    ┌─────────────────┐
                    │   Docker        │
                    │   Network       │
                    └─────────────────┘
```

## 🚀 Features

### 🎯 Core Functionality
- **Interactive Messaging**: Real-time message posting and display
- **Profile Showcase**: Personal information and tech stack display
- **Responsive Design**: Optimized for all screen sizes
- **Data Persistence**: Messages stored in MySQL database

### 🛠️ Technical Features
- **Flask Backend**: RESTful API with JSON responses
- **MySQL Integration**: Robust database connectivity with connection pooling
- **Docker Compose**: Multi-container setup with networking
- **Environment Variables**: Secure configuration management
- **Health Checks**: Container health monitoring
- **Volume Persistence**: Data survives container restarts

### 🔧 DevOps Features
- **Jenkins Pipeline**: Automated build, test, and deployment
- **AWS EC2 Deployment**: Production-ready cloud hosting
- **Docker Registry**: Container image management
- **Infrastructure as Code**: Reproducible deployments
- **Monitoring Ready**: Structured for observability tools

## 📋 Prerequisites

Before diving in, make sure you have:

### 🖥️ Local Development
- **Python 3.8+** - [Download here](https://python.org/downloads/)
- **Docker & Docker Compose** - [Get Docker](https://docs.docker.com/get-docker/)
- **Git** - [Install Git](https://git-scm.com/downloads)

### ☁️ Production Deployment
- **AWS Account** with EC2 access
- **Jenkins Server** (can be on same EC2 or separate)
- **Domain/IP** for your application
- **Basic knowledge** of Docker, AWS, and Jenkins

## 🚀 Quick Start

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/yourusername/bharath-devspace.git
cd bharath-devspace
```

### 2️⃣ Environment Setup

Create your environment file:
```bash
cp .env.example .env
# Edit .env with your database credentials
```

### 3️⃣ Local Development

**Option A: Using Docker (Recommended)**
```bash
# Start the entire application stack
docker-compose up -d

# View logs
docker-compose logs -f

# Stop the application
docker-compose down
```

**Option B: Manual Setup**
```bash
# Install dependencies
pip install -r requirement.txt

# Set environment variables
export MYSQL_HOST=localhost
export MYSQL_USER=your_user
export MYSQL_PASSWORD=your_password
export MYSQL_DB=your_database

# Run the application
python app.py
```

### 4️⃣ Access Your Application

Open your browser and navigate to:
- **Local**: `http://localhost:5000`
- **Production**: `http://your-ec2-ip:5000`

## 🐳 Docker Configuration

### Container Architecture

| Service | Image | Port | Purpose |
|---------|-------|------|----------|
| **web** | Custom Flask | 5000 | Web application |
| **db** | MySQL 8.0 | 3306 | Database server |

### Key Docker Features
- **Multi-stage builds** for optimized images
- **Health checks** for container monitoring
- **Named volumes** for data persistence
- **Custom networks** for service communication
- **Environment-based configuration**

## 🔧 Configuration

### Environment Variables

| Variable | Description | Default | Required |
|----------|-------------|---------|----------|
| `MYSQL_HOST` | Database hostname | localhost | ✅ |
| `MYSQL_USER` | Database username | root | ✅ |
| `MYSQL_PASSWORD` | Database password | - | ✅ |
| `MYSQL_DB` | Database name | devspace | ✅ |
| `FLASK_ENV` | Flask environment | production | ❌ |
| `FLASK_DEBUG` | Debug mode | False | ❌ |

### Database Schema

```sql
CREATE TABLE messages (
    id INT AUTO_INCREMENT PRIMARY KEY,
    message TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## 🚀 Deployment Guide

### AWS EC2 Deployment

1. **Launch EC2 Instance**
   ```bash
   # Amazon Linux 2 or Ubuntu 20.04 LTS recommended
   # t2.micro is sufficient for testing
   # t3.small recommended for production
   ```

2. **Install Dependencies**
   ```bash
   # Update system
   sudo yum update -y  # Amazon Linux
   # sudo apt update && sudo apt upgrade -y  # Ubuntu
   
   # Install Docker
   sudo yum install -y docker
   sudo systemctl start docker
   sudo systemctl enable docker
   sudo usermod -a -G docker ec2-user
   
   # Install Docker Compose
   sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
   sudo chmod +x /usr/local/bin/docker-compose
   ```

3. **Deploy Application**
   ```bash
   # Clone repository
   git clone <your-repo-url>
   cd bharath-devspace
   
   # Configure environment
   cp .env.example .env
   nano .env  # Edit with your settings
   
   # Start application
   docker-compose up -d
   ```

4. **Configure Security Groups**
   - Allow inbound traffic on port 5000
   - Allow SSH access (port 22) from your IP
   - Consider using Application Load Balancer for production

### Jenkins CI/CD Pipeline

The included `Jenkinsfile` provides:
- **Automated builds** on code changes
- **Docker image creation** and registry push
- **Deployment to EC2** instances
- **Health checks** and rollback capabilities

## 📁 Project Structure

```
bharath-devspace/
├── 📄 app.py                 # Flask application
├── 📄 Dockerfile            # Container definition
├── 📄 docker-compose.yml    # Multi-container setup
├── 📄 Jenkinsfile           # CI/CD pipeline
├── 📄 requirement.txt       # Python dependencies
├── 📄 message.sql           # Database schema
├── 📁 templates/            # Frontend files
│   ├── 📄 index.html        # Main HTML template
│   └── 📄 style.css         # Stylesheet
├── 📁 diagrams/             # Architecture diagrams
└── 📄 README.md             # This file
```

## 🎨 Customization

### Personalizing the Application

1. **Update Profile Information**
   ```html
   <!-- In templates/index.html -->
   <div class="name">Your Name</div>
   <div class="title">Your Title</div>
   <div class="bio">Your bio here...</div>
   ```

2. **Modify Tech Stack**
   ```html
   <!-- Add/remove tech tags -->
   <span class="tech-tag">Your Tech</span>
   ```

3. **Customize Styling**
   ```css
   /* In templates/style.css */
   /* Modify colors, fonts, animations */
   ```

## 🔍 Monitoring & Troubleshooting

### Health Checks

```bash
# Check container status
docker-compose ps

# View application logs
docker-compose logs web

# View database logs
docker-compose logs db

# Check resource usage
docker stats
```

### Common Issues

| Issue | Solution |
|-------|----------|
| **Database connection failed** | Check MySQL credentials in `.env` |
| **Port already in use** | Change port in `docker-compose.yml` |
| **Container won't start** | Check logs with `docker-compose logs` |
| **CSS not loading** | Verify file paths and Flask static config |

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

1. **Fork the repository**
2. **Create a feature branch**: `git checkout -b feature/amazing-feature`
3. **Commit your changes**: `git commit -m 'Add amazing feature'`
4. **Push to the branch**: `git push origin feature/amazing-feature`
5. **Open a Pull Request**

### Development Guidelines
- Follow PEP 8 for Python code
- Use meaningful commit messages
- Add comments for complex logic
- Test your changes locally
- Update documentation as needed

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **Flask Community** for the amazing web framework
- **Docker** for containerization technology
- **AWS** for reliable cloud infrastructure
- **Jenkins** for CI/CD automation
- **Open Source Community** for inspiration and tools

## 📞 Contact & Support

**Bharath Aaleti**
- 💼 DevOps Engineer at Accenture
- 🌐 LinkedIn: [Connect with me](https://linkedin.com/in/bharath-aaleti)
- 📧 Email: bharath.aaleti@example.com
- 🐙 GitHub: [@bharath-aaleti](https://github.com/bharath-aaleti)

---

<div align="center">

**⭐ If you found this project helpful, please give it a star! ⭐**

*Built with ❤️ by Bharath Aaleti*

</div>
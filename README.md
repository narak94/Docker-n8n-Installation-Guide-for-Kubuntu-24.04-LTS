<div align="center">

# 🐳 Docker + n8n Installation Guide for Kubuntu 24.04 LTS

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Kubuntu](https://img.shields.io/badge/Kubuntu-24.04%20LTS-blue)](https://kubuntu.org/)
[![Docker](https://img.shields.io/badge/Docker-Latest-2496ED?logo=docker)](https://www.docker.com/)
[![n8n](https://img.shields.io/badge/n8n-Latest-EA4B71?logo=n8n)](https://n8n.io/)

**Complete step-by-step guide to install Docker Engine, Docker Compose, and n8n on Kubuntu 24.04 LTS Noble**

[English](README.md) • [Português](README-pt-BR.md)

</div>

---

## 📋 Table of Contents

- [About](#about)
- [Prerequisites](#prerequisites)
- [Quick Start](#quick-start)
- [Installation Steps](#installation-steps)
- [System Update](#system-update)
- [Docker Engine](#docker-engine)
- [Docker Compose](#docker-compose)
- [n8n Setup](#n8n-setup)
- [Usage](#usage)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)
- [Acknowledgments](#acknowledgments)

---

## 🎯 About

This guide provides a comprehensive, step-by-step tutorial for installing Docker Engine, Docker Compose, and n8n workflow automation tool on Kubuntu 24.04 LTS Noble. Perfect for beginners and experienced users alike.

### What You'll Get

- ✅ Fully updated Kubuntu system
- ✅ Docker Engine with best practices
- ✅ Docker Compose V2
- ✅ n8n running in a container
- ✅ Production-ready configuration
- ✅ Useful commands and troubleshooting tips

---

## 📦 Prerequisites

- Kubuntu 24.04 LTS Noble installed
- Terminal access with sudo privileges
- Stable internet connection
- At least 2GB of free disk space

---

## ⚡ Quick Start

For experienced users, here's the TL;DR:
```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Install Docker
curl -fsSL https://get.docker.com | sh
sudo usermod -aG docker $USER

# Start n8n
docker run -d --restart unless-stopped --name n8n -p 5678:5678 -v ~/.n8n:/home/node/.n8n n8nio/n8n
```

Access n8n at: `http://localhost:5678`

> 💡 For detailed instructions with explanations, see the [full guide](#installation-steps) below.

---

## 📚 Installation Steps

### System Update

First, let's update your Kubuntu system:
```bash
# Update package list
sudo apt update

# Upgrade all installed packages
sudo apt upgrade -y

# Remove unnecessary packages
sudo apt autoremove -y
```

> 📖 **See detailed guide:** [docs/installation.md](docs/installation.md)

### Docker Engine

Install Docker Engine with official repositories:
```bash
# Install dependencies
sudo apt install -y ca-certificates curl gnupg lsb-release

# Add Docker's GPG key
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# Install Docker
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

[Read full Docker installation guide →](docs/installation.md#docker-engine)

### Docker Compose

Docker Compose V2 is included with Docker Engine. Verify installation:
```bash
docker compose version
```

### n8n Setup

#### Option 1: Quick Setup (Single Command)
```bash
docker run -d --restart unless-stopped \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n
```

#### Option 2: Docker Compose (Recommended)

Create `docker-compose.yml`:
```yaml
version: '3.8'

services:
  n8n:
    image: n8nio/n8n
    container_name: n8n
    restart: unless-stopped
    ports:
      - "5678:5678"
    environment:
      - N8N_BASIC_AUTH_ACTIVE=true
      - N8N_BASIC_AUTH_USER=admin
      - N8N_BASIC_AUTH_PASSWORD=change_this_password
    volumes:
      - ~/.n8n:/home/node/.n8n
```

Start n8n:
```bash
docker compose up -d
```

---

## 🚀 Usage

### Accessing n8n

Open your browser and navigate to:
```
http://localhost:5678
```

### Common Commands
```bash
# View running containers
docker ps

# View n8n logs
docker logs n8n -f

# Stop n8n
docker stop n8n

# Start n8n
docker start n8n

# Update n8n
docker pull n8nio/n8n
docker restart n8n
```

---

## 🔧 Troubleshooting

### Permission Denied Error
```bash
sudo usermod -aG docker $USER
newgrp docker
```

### Port Already in Use
```bash
# Check what's using port 5678
sudo lsof -i :5678

# Change port in docker-compose.yml
ports:
  - "8080:5678"
```

> 📖 **More solutions:** [docs/troubleshooting.md](docs/troubleshooting.md)

---

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

See [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- [Docker Documentation](https://docs.docker.com/)
- [n8n Documentation](https://docs.n8n.io/)
- [Kubuntu Community](https://kubuntu.org/)
- All contributors who help improve this guide

---

## 📞 Support

If you found this guide helpful, please consider:

- ⭐ Starring this repository
- 🐛 Reporting bugs via [Issues](https://github.com/yourusername/docker-n8n-kubuntu/issues)
- 💬 Sharing your feedback

---

<div align="center">

**Made with ❤️ for the community**

[Report Bug](https://github.com/yourusername/docker-n8n-kubuntu/issues) • 
[Request Feature](https://github.com/yourusername/docker-n8n-kubuntu/issues)

</div>

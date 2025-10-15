<div align="center">

# 🐳 Guia de Instalação Docker + n8n para Kubuntu 24.04 LTS

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Kubuntu](https://img.shields.io/badge/Kubuntu-24.04%20LTS-blue)](https://kubuntu.org/)
[![Docker](https://img.shields.io/badge/Docker-Latest-2496ED?logo=docker)](https://www.docker.com/)
[![n8n](https://img.shields.io/badge/n8n-Latest-EA4B71?logo=n8n)](https://n8n.io/)

**Guia completo passo a passo para instalar Docker Engine, Docker Compose e n8n no Kubuntu 24.04 LTS Noble**

[English](README.md) • [Português](README-pt-BR.md)

</div>

---

## 📋 Índice

- [Sobre o Projeto](#sobre-o-projeto)
- [Pré-requisitos](#pré-requisitos)
- [Início Rápido](#início-rápido)
- [Passos de Instalação](#passos-de-instalação)
- [Atualização do Sistema](#atualização-do-sistema)
- [Docker Engine](#docker-engine)
- [Docker Compose](#docker-compose)
- [Configuração do n8n](#configuração-do-n8n)
- [Como Usar](#como-usar)
- [Solução de Problemas](#solução-de-problemas)
- [Contribuindo](#contribuindo)
- [Licença](#licença)
- [Agradecimentos](#agradecimentos)

---

## 🎯 Sobre o Projeto

Este guia fornece um tutorial completo e detalhado para instalar Docker Engine, Docker Compose e a ferramenta de automação de workflows n8n no Kubuntu 24.04 LTS Noble. Perfeito tanto para iniciantes quanto para usuários experientes.

### O que Você Vai Conseguir

- ✅ Sistema Kubuntu totalmente atualizado
- ✅ Docker Engine com melhores práticas
- ✅ Docker Compose V2 configurado
- ✅ n8n rodando em container
- ✅ Configuração pronta para produção
- ✅ Comandos úteis e dicas de solução de problemas

---

## 📦 Pré-requisitos

- Kubuntu 24.04 LTS Noble instalado
- Acesso ao terminal com privilégios sudo
- Conexão estável com a internet
- Pelo menos 2GB de espaço livre em disco

---

## ⚡ Início Rápido

Para usuários experientes, aqui está o resumo:
```bash
# Atualizar sistema
sudo apt update && sudo apt upgrade -y

# Instalar Docker
curl -fsSL https://get.docker.com | sh
sudo usermod -aG docker $USER

# Iniciar n8n
docker run -d --restart unless-stopped --name n8n -p 5678:5678 -v ~/.n8n:/home/node/.n8n n8nio/n8n
```

Acesse o n8n em: `http://localhost:5678`

> 💡 Para instruções detalhadas com explicações, veja o [guia completo](#passos-de-instalação) abaixo.

---

## 📚 Passos de Instalação

### Atualização do Sistema

Primeiro, vamos atualizar seu sistema Kubuntu:
```bash
# Atualizar lista de pacotes
sudo apt update

# Atualizar todos os pacotes instalados
sudo apt upgrade -y

# Remover pacotes desnecessários
sudo apt autoremove -y
```

> 📖 **Veja o guia detalhado:** [docs/installation.md](docs/installation.md)

### Docker Engine

Instalar Docker Engine com repositórios oficiais:
```bash
# Instalar dependências
sudo apt install -y ca-certificates curl gnupg lsb-release

# Adicionar chave GPG do Docker
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# Instalar Docker
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

[Leia o guia completo de instalação do Docker →](docs/installation.md#docker-engine)

### Docker Compose

Docker Compose V2 já vem incluído com o Docker Engine. Verifique a instalação:
```bash
docker compose version
```

### Configuração do n8n

#### Opção 1: Configuração Rápida (Comando Único)
```bash
docker run -d --restart unless-stopped \
  --name n8n \
  -p 5678:5678 \
  -v ~/.n8n:/home/node/.n8n \
  n8nio/n8n
```

#### Opção 2: Docker Compose (Recomendado)

Crie o arquivo `docker-compose.yml`:
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
      - N8N_BASIC_AUTH_PASSWORD=troque_esta_senha
    volumes:
      - ~/.n8n:/home/node/.n8n
```

Inicie o n8n:
```bash
docker compose up -d
```

---

## 🚀 Como Usar

### Acessando o n8n

Abra seu navegador e acesse:
```
http://localhost:5678
```

### Comandos Comuns
```bash
# Ver containers rodando
docker ps

# Ver logs do n8n
docker logs n8n -f

# Parar n8n
docker stop n8n

# Iniciar n8n
docker start n8n

# Atualizar n8n
docker pull n8nio/n8n
docker restart n8n
```

---

## 🔧 Solução de Problemas

### Erro de Permissão Negada
```bash
sudo usermod -aG docker $USER
newgrp docker
```

### Porta Já em Uso
```bash
# Verificar o que está usando a porta 5678
sudo lsof -i :5678

# Mudar porta no docker-compose.yml
ports:
  - "8080:5678"
```

> 📖 **Mais soluções:** [docs/troubleshooting.md](docs/troubleshooting.md)

---

## 🤝 Contribuindo

Contribuições são bem-vindas! Sinta-se à vontade para enviar um Pull Request.

1. Faça um Fork do repositório
2. Crie sua branch de feature (`git checkout -b feature/NovaFuncionalidade`)
3. Faça commit das suas mudanças (`git commit -m 'Adiciona nova funcionalidade'`)
4. Faça push para a branch (`git push origin feature/NovaFuncionalidade`)
5. Abra um Pull Request

Veja [CONTRIBUTING.md](CONTRIBUTING.md) para diretrizes detalhadas.

---

## 📄 Licença

Este projeto está licenciado sob a Licença MIT - veja o arquivo [LICENSE](LICENSE) para detalhes.

---

## 🙏 Agradecimentos

- [Documentação Docker](https://docs.docker.com/)
- [Documentação n8n](https://docs.n8n.io/)
- [Comunidade Kubuntu](https://kubuntu.org/)
- Todos os contribuidores que ajudam a melhorar este guia

---

## 📞 Suporte

Se este guia foi útil para você, considere:

- ⭐ Dar uma estrela neste repositório
- 🐛 Reportar bugs via [Issues](https://github.com/seuusuario/docker-n8n-kubuntu/issues)
- 💬 Compartilhar seu feedback

---

<div align="center">

**Feito com ❤️ para a comunidade**

[Reportar Bug](https://github.com/seuusuario/docker-n8n-kubuntu/issues) • 
[Solicitar Funcionalidade](https://github.com/seuusuario/docker-n8n-kubuntu/issues)

</div>
```

---


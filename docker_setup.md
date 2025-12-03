# Docker Installation (Debian)

This guide installs the latest stable Docker Engine, CLI, Buildx, and Compose plugin.

---

## 1. Update System & Install Prerequisites

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install ca-certificates curl gnupg lsb-release -y
```

---

## 2. Add Docker GPG Key & Repository

```bash
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian $(. /etc/os-release && echo \"$VERSION_CODENAME\") stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
```

---

## 3. Install Docker Engine, CLI, Buildx, and Compose Plugin

```bash
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
```

---

## 4. Verify Installation

```bash
sudo systemctl status docker
sudo docker run hello-world
```

---

## 5. Optional: Allow Non-Root Docker Usage

```bash
sudo usermod -aG docker $USER
# Log out and log back in to apply group changes
```

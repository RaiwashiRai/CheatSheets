# vm-ssh-setup.md

# VM + SSH Setup Cheat Sheet

This guide helps you start a Debian VM headless, set up NAT & port forwarding for SSH, and enable a colored shell prompt.

---

## 1. Set NAT + Port Forwarding

```bash
VBoxManage modifyvm my-debian-vm --natpf1 "guestssh,tcp,,2222,,22"
```

Forward host port `2222` to VM port `22`.

### or

### Configure the VM to use NAT with port forwarding

1. Power off your VM.

2. In VirtualBox → Settings → Network → Adapter 1 → Attached to: NAT.

3. Click Advanced → Port Forwarding.

4. Add a rule:
    - Name: SSH
    - Protocol: TCP
    - Host IP: 127.0.0.1
    - Host Port: 2222
    - Guest IP: leave blank
    - Guest Port: 22

5. Save and start the VM.

This guarantees your host can reach the VM via localhost without worrying about the VM’s IP.

---

## 2. Start VM Headless

```bash
VBoxManage startvm my-debian-vm --type headless
```

---

## 3. Connect via SSH with Color Support

```bash
export TERM=xterm-256color
ssh -p 2222 ryu@127.0.0.1
```

---

## 4. Enable Colored Prompt in VM (Bash)

Add to `~/.bashrc`:

```bash
PS1="\[\e[32m\]\u@\h \[\e[34m\]\w \$\[\e[0m\]"
alias ls='ls --color=auto'
```

---

## 5. Optional: Install Zsh + Oh-My-Zsh

```bash
sudo apt install zsh git curl -y
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
chsh -s $(which zsh)
```

---

# docker-setup.md

# Docker Installation Cheat Sheet (Debian)

This guide installs the latest stable Docker engine, CLI, Buildx, and Compose plugin.

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

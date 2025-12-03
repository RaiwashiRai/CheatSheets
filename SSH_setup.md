# VM + SSH Setup

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

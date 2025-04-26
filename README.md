# 🛜 Linux Proxy Applier - IIITA

Simple scripts to quickly set and remove system-wide proxy settings on GNU/Linux systems.

> ⚠️ Please read carefully before using.

---

## 📋 Before You Start

- **Backup** your `/etc/environment` file:
  ```bash
  sudo cp /etc/environment ~/environment.backup
Do not run these scripts using sudo.

Works best on Debian-based distributions like Ubuntu, Kubuntu, Pop!_OS, Linux Mint, etc.

🚀 How to Use
- Set Proxy:
  ```bash
  ./apply_proxy

You’ll be asked to enter the proxy hostname.

- Remove Proxy:
  ```bash
  ./remove_proxy
  
🖥️ If you are using KDE Plasma, enable:
System Settings → Network → Settings → Proxy → Use system proxy configuration

🌎 Run Scripts from Anywhere

- If you want to use apply_proxy and remove_proxy globally, add them to your ~/.local/bin/:
  ```bash
  mkdir -p ~/.local/bin
  
  curl https://raw.githubusercontent.com/Surya-Raghuram/Linux-Proxy/main/linux-proxy/apply_proxy > ~/.local/bin/apply_proxy && chmod +x ~/.local/bin/apply_proxy
  curl https://raw.githubusercontent.com/Surya-Raghuram/Linux-Proxy/main/linux-proxy/remove_proxy > ~/.local/bin/remove_proxy && chmod +x ~/.local/bin/remove_proxy
  
✅ After this, you can run apply_proxy or remove_proxy from any directory!

🔍 What the Scripts Modify
When you apply proxy, the script updates:
- ```bash
  /etc/environment

snap proxy settings
- ```bash
  /etc/apt/apt.conf
  
⚡ Important Warnings

   Modifying /etc/environment is risky. Always keep a backup.

  Understand what the script does before running it.

  If something goes wrong, it's on you — use responsibly.

📢 Suggestions or Issues?
  Feel free to create an issue on this repository.


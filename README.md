# 🛜 Linux Proxy Applier - IIITA

Simple scripts to quickly set and remove system-wide proxy settings on GNU/Linux systems.

> ⚠️ Please read carefully before using.

---

## 📋 Before You Start

- **Backup** your `/etc/environment` file:
  ```bash
  sudo cp /etc/environment ~/environment.backup
Do not run these scripts using sudo.

⚠️ Currently tested and supported only on **Debian-based distributions** (Ubuntu, Kubuntu, Pop!_OS, Linux Mint, etc.).  
Other distros like Arch, Fedora, or openSUSE are **not yet supported**.  

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

  ## 📝 TODO

- [ ] Add support for Arch-based distros (Manjaro, EndeavourOS, Arch Linux)  
- [ ] Add support for Fedora/RHEL/CentOS (DNF/YUM proxy configs)  
- [ ] Add GNOME/KDE desktop environment proxy integration  
- [ ] Export proxy settings in shell configs (~/.bashrc, ~/.zshrc, etc.)  
- [ ] Add dry-run mode + rollback option for safety  
- [ ] Provide `.deb` and `.rpm` packages for easier installation  

📢 Suggestions or Issues?
  Feel free to create an issue on this repository.


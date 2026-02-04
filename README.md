# 🚨 Edit Guardian Bot
A powerful Telegram bot built with **Python** to protect your groups from edited messages.  
It automatically deletes edited messages to maintain transparency and keeps you notified when any message is removed.

---

## ✨ Features
- 🔹 **Auto-delete edited messages** in groups  
- 🔹 **Instant notifications** for deleted messages  
- 🔹 **Easy setup** — just add to your group and start  
- 🔹 **Customizable** via environment variables  
- 🔹 Works 24/7 on **Heroku**  

---

## 🚀 Deployment

### Heroku (One-Click Deploy)
Click the button below to deploy directly to Heroku:

<p align="center">
  <a href="https://dashboard.heroku.com/new?template=https://github.com/riteshxcoder/EDITGUARDIAN">
    <img src="https://img.shields.io/badge/Deploy%20On%20Heroku-7056bf?style=for-the-badge&logo=heroku&logoColor=white" width="220" height="38"/>
  </a>
</p>

---

# Update system
sudo apt update && sudo apt upgrade -y

# Install dependencies
sudo apt install -y python3 python3-pip python3-venv git

# Clone repo
git clone https://github.com/Aashik-team/EDITGUARDIAN
cd Aashik-Edit

# Create virtual environment
python3 -m venv venv

# Install requirements
pip install --upgrade pip
pip install -r requirements.txt

# Test run (check bot is working)
python3 main.py

# ---- Setup systemd service (background run) ----
sudo bash -c 'cat > /etc/systemd/system/editguardian.service <<EOF
[Unit]
Description=Telegram Edit Guardian Bot
After=network.target

[Service]
User=ubuntu
WorkingDirectory=/opt/Aashik-Edit
EnvironmentFile=/opt/Aashik-Edit/.env
ExecStart=/opt/Aashik-Edit/venv/bin/python /opt/Aashik-Edit/main.py
Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
EOF'

# Reload services and enable bot auto-start
sudo systemctl daemon-reload
sudo systemctl enable editguardian
sudo systemctl start editguardian

# Check logs (optional)
sudo systemctl status editguardian
journalctl -u editguardian -f

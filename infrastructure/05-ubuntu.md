# 05 ubuntu

---


```markdown
# Ubuntu Server

## Install SSH

```bash
sudo apt update
sudo apt install openssh-server -y

Check Logs

sudo tail -f /var/log/auth.log


Install Wazuh Agent

curl -s https://packages.wazuh.com | sudo bash


Restart Agent

sudo systemctl restart wazuh-agent

Purpose:
ssh brute force detection
Linux Log Monitoring

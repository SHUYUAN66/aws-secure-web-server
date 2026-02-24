# AWS Secure Web Server Deployment (Nginx on EC2)

A hands-on cloud + Linux project that deploys a production-style Nginx web server on AWS EC2 with security hardening, least-privilege access, and basic monitoring.

---

## Architecture (High Level)

User Browser → **Internet** → **AWS Security Group (Firewall)** → **EC2 (Linux)** → **Nginx (Web Server)**

**AWS Components**

* **EC2**: Linux virtual machine hosting Nginx
* **Security Group**: inbound rules allow only required ports
* **IAM**: least-privilege access for administration
* **CloudWatch**: basic metrics/monitoring for the instance

---

## Security Controls Implemented

### Network / Access Control

* Inbound ports exposed: **80 (HTTP)**, **443 (HTTPS)**
* SSH (**22**) is restricted (e.g., only from my IP or a trusted network)

### Identity & Permissions (IAM)

* Followed **least-privilege** principles (no unnecessary admin permissions)

### Server Hardening (Linux)

* Disabled **root SSH login**
* Enforced **key-based authentication**
* Configured **UFW** firewall rules
* Scheduled basic log review using **cron**

> Note: Sensitive information (public IPs, account IDs, keys) should be removed or masked before publishing.

---

## Deployment Steps (Reproducible)

### 1) Provision EC2

* Launch an EC2 instance (Linux)
* Create or select an SSH key pair
* Configure Security Group:

  * Allow **80/443** from the internet
  * Allow **22** only from a trusted source (e.g., your public IP)

### 2) Connect via SSH

```bash
ssh -i <your-key.pem> <user>@<ec2-public-ip>
```

### 3) Install and start Nginx

```bash
sudo apt update
sudo apt install -y nginx
sudo systemctl enable nginx
sudo systemctl start nginx
sudo systemctl status nginx
```

### 4) Verify web access

* Open: `http://<ec2-public-ip>`
* You should see the Nginx welcome page (or your custom page)

### 5) Basic SSH hardening (example)

* Disable root login and enforce key auth in SSH config, then restart SSH:

```bash
sudo systemctl restart ssh
```

### 6) Enable firewall (UFW example)

```bash
sudo ufw allow OpenSSH
sudo ufw allow 'Nginx Full'
sudo ufw enable
sudo ufw status
```

---

## Monitoring & Troubleshooting

### Check service status

```bash
sudo systemctl status nginx
```

### View logs (common when debugging)

```bash
sudo journalctl -u nginx --no-pager -n 100
```

### CloudWatch

* Monitor instance metrics such as CPU usage and network throughput
* Use metrics to detect abnormal usage and validate stability

---

## Evidence (Screenshots)

Screenshots and evidence are stored in: **docs/**

* EC2 instance running
* Security Group rules (only 80/443 open; SSH restricted)
* Nginx accessible from browser
* CloudWatch metrics
* SSH hardening proof
* UFW status/rules

See: `docs/README.md`

---

## What I Learned

* How to deploy a web server on AWS and expose only required network ports
* How to apply least-privilege IAM and reduce the attack surface
* How to harden SSH access and operate a Linux service using system tools
* How to monitor and troubleshoot services using logs and CloudWatch

# AWS Secure Web Server Deployment (Nginx on EC2)

A hands-on cloud + Linux project that deploys a production-style Nginx web server on AWS EC2 with security hardening, least-privilege access, and basic monitoring.

## What I built

* Provisioned an AWS EC2 Linux instance and deployed an Nginx web service
* Configured Security Group rules to restrict SSH access and expose only required ports (80/443)
* Applied IAM least-privilege principles for secure administration
* Monitored Nginx and EC2 health using `systemctl`, `journalctl`, and AWS CloudWatch
* Hardened SSH access (disabled root login, enforced key-based auth) and configured firewall rules (UFW)
* Automated basic log review with `cron`

## Tech Stack

* AWS: EC2, Security Groups, IAM, CloudWatch
* OS/Tools: Linux, SSH, UFW, systemd (`systemctl` / `journalctl`)
* Web Server: Nginx

## Repository Plan

* `docs/` — screenshots and evidence (AWS console, CloudWatch, security rules)
* `scripts/` — setup/hardening/log review scripts
* `nginx/` — sample Nginx configs

## Notes

Sensitive information (public IPs, account IDs, keys) should be removed or masked before uploading screenshots or configs.

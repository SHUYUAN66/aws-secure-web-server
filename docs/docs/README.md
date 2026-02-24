# Evidence / Screenshots (Docs)

This folder contains screenshots and evidence to validate the deployment and security controls.

## Recommended evidence checklist

* EC2 instance running (AWS Console)
* Security Group rules (only 80/443 open; SSH restricted)
* Nginx page accessible in browser
* CloudWatch metrics / alarms (CPU, network, etc.)
* SSH hardening proof (`PermitRootLogin no`, key-based auth)
* UFW status and rules

> IMPORTANT: Mask sensitive information (public IPs, account IDs, usernames, key paths).

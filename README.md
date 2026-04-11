# internship task: implement endpoint security & monitoring

## objective
protect internee.pk’s devices and servers from malware and unauthorized access by deploying **wazuh** as an endpoint detection and response (edr) solution.  

this documentation covers the installation of wazuh server, dashboard access, and ongoing agent setup. further steps will include monitoring file integrity, user activity, and automating alerts.

---

## environment setup
**virtual machine configuration (oracle virtualbox):**
- os: ubuntu 24.04.1 lts (64‑bit)  
- base memory: 6125 mb  
- video memory: 16 mb  
- graphics controller: vmsvga  
- chipset: piix3  
- secure boot: disabled  

<img width="1919" height="1101" alt="wazuh-server-settings" src="https://github.com/user-attachments/assets/cc6cd988-7fef-4d1a-8b58-683eab1e6706" />


---

## system preparation
update and upgrade packages:

```bash
sudo apt update && sudo apt upgrade -y
```

<img width="1919" height="1153" alt="ubuntu-installed" src="https://github.com/user-attachments/assets/ce90ed35-3ac3-465e-abf0-e7ce2e1b0056" />


---

## wazuh installation
installation performed using the official wazuh script:

```bash
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
sudo bash wazuh-install.sh -a -i
```

**components installed:**
- wazuh indexer  
- wazuh manager  
- filebeat  
- wazuh dashboard  

<img width="1919" height="1146" alt="wazuh-installed" src="https://github.com/user-attachments/assets/725187e0-b77e-461e-809e-62ec715fd410" />


---

## dashboard access
dashboard available at:

```
https://localhost:4433/app/wazuh
```

**login screen:**  
- username: admin  
- password: generated during installation  

<img width="1867" height="1042" alt="wazuh-login" src="https://github.com/user-attachments/assets/fb10a5ec-039c-404a-8070-302a8eba07cf" />


**overview page:**  
- total agents: 0 (pending setup)  
- modules:  
  - security events  
  - integrity monitoring  
  - policy auditing  
  - vulnerabilities  
  - compliance frameworks  

<img width="1881" height="1109" alt="wazuh-dashboard" src="https://github.com/user-attachments/assets/de3c996d-19a6-4261-a18b-8963031a8884" />


---

## agent setup (in progress)
current step: installing wazuh agent to connect with the manager.  

**command (on endpoint):**
```bash
curl -sO https://packages.wazuh.com/4.7/wazuh-agent.sh
sudo bash wazuh-agent.sh -a <manager-ip> -p 1514
```

verify agent status:
```bash
sudo systemctl status wazuh-agent
```

*(screenshot: agent installation will be added once complete)*

---

## next steps
- complete agent registration and confirm connectivity in dashboard  
- configure integrity monitoring and auditing policies  
- integrate sysmon logs for endpoint visibility  
- connect malwarebazaar feeds for threat intelligence  
- test automated alerts for suspicious activity  

---

## references
- virtualbox manual  
- ubuntu server guide 
- wazuh documentation
- malwarebazaar dataset 
 
---



# Programmatic Vulnerability Remediation Project

This project is about remediating a Linux VM with the following vulnerabilities using DISA STIG Compliance vulnerability scan:
- Default Root Password - Enabled. 
- Telnet - Enabled.
- OpenSSL 


![Linux](https://github.com/user-attachments/assets/8f05ea1c-10e9-4956-a16b-b3533f7c57ad)

---
# Tools & Technology:
- Tenable (enterprise vulnerability management platform)
- Azure Virtual Machine
- Bash 


---
# Table of contents

- [Step 1) Provision virtual machine in the Azure portal](#step-1-provision-virtual-machine-in-the-azure-portal)
- [Step 2) Log into the VM and disable the Windows Firewall](#step-2-log-into-the-vm-and-disable-the-windows-firewall)
- [Step 3) Login to tenable](#step-3-login-to-tenable)
- [Step 4) Create a Custom Scan](#step-4-create-a-custom-scan)
- [Step 5) Remediation Implementation](#step-5-remediation-implementation)
- [Step 6) Scan Results After Remediation](#step-6-scan-results-after-remediation)
---


### Step 1) Provision virtual machine in the Azure portal

<img width="700" alt="vm7" src="https://github.com/user-attachments/assets/e3f43af8-ff41-4694-b1de-7c4cfff4d1ba" />

---
### Step 2)  Login to tenable

<img width="400" alt="tenablelogin" src="https://github.com/user-attachments/assets/65aa3c73-113b-4b85-8b79-de3a142d4e4b" />

---

### Step 3) Create a User Defined Template

#### Select Linux Vulnerabilities DISA STIG Template

<img width="700" alt="scan" src="https://github.com/user-attachments/assets/46931302-9dca-47e5-a17c-0ef05a64b08b" />


#### Configure Scan Basic settings

<img width="700" alt="credentials" src="https://github.com/user-attachments/assets/18a0ca1f-7065-4e2a-9d10-8c28267efaf0" />

#### Configure Scan Credential settings

<img width="700" alt="credentials" src="https://github.com/user-attachments/assets/03528eb3-9c7c-4d43-8d6e-708b71e7262f" />


#### Initial Baseline Scan Results
<img width="700" alt="scan results" src="https://github.com/user-attachments/assets/c1963fa0-9179-40d4-b16d-12c2bf5c9ce2" />

#### [Tenable Vulnerability Management Report - Initial](https://drive.google.com/file/d/1kLms34Q2ugVYL5-4Q0IHXvQVsvof4iAF/view?usp=drive_link)
---
### Step 5) Create the Vulnerabilities 
#### a. Log into your VM with SSH and install and Start Telnet (insecure 3rd party application):
sudo apt update (to upgrade installed packages)
sudo apt install telnetd -y (to install telnet server)
sudo systemctl enable inetd.service (enables the inetd service so it will start automatically every time the system boots)
sudo systemctl start inetd.service (starts the inetd service immediately)

sudo systemctl status inetd.service (check if it successfully started)

<img width="400" alt="scan results" src="https://github.com/user-attachments/assets/852e5d1e-0d7e-4e83-b4cb-66eb4591a119" />

#### b. Log into your VM with SSH and enable the root account and allow SSH login with root: 
sudo grep -q '^PermitRootLogin' /etc/ssh/sshd_config && sudo sed -i 's/^PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config || echo 'PermitRootLogin yes' | sudo tee -a /etc/ssh/sshd_config && sudo systemctl restart sshd

Log into your VM with SSH and set the root password to “root” (Insecure OS configuration):
sudo passwd root

---

### Step 5) Remediation : Use the bash scripts to automatically remediate vulnerabilities

##### Remediate Default Root Password:

<img width="400" alt="scan results" src="https://github.com/user-attachments/assets/8bb0add0-ae35-411e-bdcd-f267df0f28fe" />


[Remediation PowerShell Script](remediation/remediation-FireFox-uninstall.ps1)

##### Remediate SMB v1
<img width="400" alt="scan results" src="https://github.com/user-attachments/assets/2c974f26-b78f-47d3-92cc-1c8a1f647c02" />

[Remediation Powershell Script](remediation/remediation-SMBv1.ps1)


##### Remediate discouraged cryptographic protocols
<img width="400" alt="scan results" src="https://github.com/user-attachments/assets/72b61abf-5959-4ab0-8ed5-b992bdf36cbf" />


[Remediation Powershell Script](https://github.com/fesguerra143/automation/blob/cc635a606dfa9d55829f1b4ffbe6a9d34a4debad/toggle-protocols.ps1)



---

### Step 6) Scan Results After Remediation

<img width="700" alt="scan results" src="https://github.com/user-attachments/assets/2cf0f6bb-51c9-4052-9649-7a3049937a0e" />

#### Tenable Vulnerability Management Report
[Tenable Vulnerability Management Report](https://drive.google.com/file/d/1wsiYlNjNFqvXqji4pbG02z2_a-n1-Hs_/view?usp=drive_link)


---

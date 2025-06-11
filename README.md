

# Programmatic Vulnerability Remediation Project

This project is about remediating a Linux VM with the following vulnerabilities using DISA STIG Compliance vulnerability scan:
- Default Root Password  
- Telnet 
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
- [Step 2)  Login to tenable](#step-2--login-to-tenable)
- [Step 3) Create a User Defined Template](#step-3-create-a-user-defined-template)
- [Step 4) Create the Vulnerabilities](#step-4-create-the-vulnerabilities)
- [Step 5) Remediation](#step-5-remediation-)
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

---
### Step 4) Create the Vulnerabilities 
#### a. Log into your VM with SSH and install and Start Telnet (insecure 3rd party application):
sudo apt update (to upgrade installed packages) <br />
sudo apt install telnetd -y (to install telnet server)<br />
sudo systemctl enable inetd.service (enables the inetd service so it will start automatically every time the system boots)<br />
sudo systemctl start inetd.service (starts the inetd service immediately)<br />

sudo systemctl status inetd.service (check if it successfully started)

<img width="400" alt="scan results" src="https://github.com/user-attachments/assets/852e5d1e-0d7e-4e83-b4cb-66eb4591a119" />

#### b. Log into your VM with SSH and enable the root account and allow SSH login with root: 
sudo grep -q '^PermitRootLogin' /etc/ssh/sshd_config && sudo sed -i 's/^PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config || echo 'PermitRootLogin yes' | sudo tee -a /etc/ssh/sshd_config && sudo systemctl restart sshd <br />

Log into your VM with SSH and set the root password to “root” (Insecure OS configuration):<br />
sudo passwd root

#### Scan Results After creation of vulnerabilities
<img width="700" alt="scan results" src="https://github.com/user-attachments/assets/9021d1ae-480e-4d40-adb3-e0a243dc6d82" />


#### [Tenable Vulnerability Management Report - Initial](https://drive.google.com/file/d/1Cffv00gtI8SsYUPoXFCJLBRIm_zuuP3y/view?usp=sharing)

---

### Step 5) Remediation : 

##### Remediate Default Root Password:

<img width="600" alt="scan results" src="https://github.com/user-attachments/assets/1ba0f896-fa36-4870-88bf-9769a4497611" />

[Remediation Script](https://github.com/fesguerra143/automation/blob/414385b6496cc98f2ae3ed6e5cd39eb4ea03edf9/remediation-root-password.sh)

##### Remediate OpenSSL:
<img width="600" alt="scan results" src="https://github.com/user-attachments/assets/0b0110bf-07b7-4d27-b5d1-abf7f82ff4d2" />

[Remediation Script](https://github.com/fesguerra143/automation/blob/414385b6496cc98f2ae3ed6e5cd39eb4ea03edf9/remediation-openssl-3.0.5-install.sh)

##### Remediate Telnet:
<img width="600" alt="scan results" src="https://github.com/user-attachments/assets/b98e7f03-a081-40d4-a0cc-bfaea1d1f736" />

[Remediation Script](https://github.com/fesguerra143/automation/blob/414385b6496cc98f2ae3ed6e5cd39eb4ea03edf9/remediation-Telnet-Remove.sh)

---

### Step 6) Scan Results After Remediation

<img width="700" alt="scan results" src="https://github.com/user-attachments/assets/cbce78c3-53b1-4eba-a198-b79ac6f44c1f" />

#### Tenable Vulnerability Management Report
[Tenable Vulnerability Management Report - Final ](https://drive.google.com/file/d/1ID-hSem0YbmA8_20D-kyk4JWR9_TPJ_l/view?usp=drive_link)

---

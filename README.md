# 🔐 Site-to-Site VPN & Network Security Implementation Using pfSense  

This project demonstrates a hands-on **Network Security Implementation** using **pfSense** to establish a secure **Site-to-Site IPsec VPN tunnel** between two remote virtual networks.  
It simulates an enterprise-grade network environment focused on encrypted data transfer, firewall configuration, and secure connectivity validation.

---

## 🎯 Project Overview  

The objective of this project was to design, implement, and test a secure network communication channel between **two branch offices** using **pfSense firewalls**.  
The lab setup ensures data confidentiality, integrity, and availability through **AES-256 encryption**, **SHA-256 hashing**, and **IPsec protocols**.

---

## 🧩 Technologies Used  

This project was developed and tested using the following tools:  
- **Oracle VirtualBox:** Version 7.1.2  
- **pfSense Firewall:** Version 2.7.2 (Community Edition ISO)  
- **Wireshark:** Version 4.4.2  
- **Ubuntu Desktop:** 24.04 LTS (Client VM)
- **Linux Mint:** 21.3 (Victoria Edition)  
- **Kali Linux:** 2024.3 (Testing and Security Validation)  
- **Windows 10 Pro (Evaluation):** Used as secondary client VM  

**Hardware used:**  
- Intel i5 (11th Gen), 16GB RAM, 512GB SSD  
- Network: VirtualBox Internal Networks (SecureNet / WANNet)  

All virtual machines were created using Oracle VirtualBox on Windows 11 host.  
Each pfSense firewall used **2 virtual adapters** — one for WAN and one for LAN.

---

### 🖥️ Network Hosts Summary  

**Site A (Head Office / Left Network)**  
- **pfSense A Firewall:** WAN – 10.10.10.1  |  LAN – 192.168.50.1  
- **Ubuntu Desktop (Client):** 192.168.50.10 (Static IP)  
  - Role: Used to test VPN connectivity and cross-site communication  
  - OS Version: Ubuntu 24.04 LTS  
- **Kali Linux (Client):** 192.168.50.11 (Static IP)  
  - Role: Used for penetration testing, packet capture, and security validation  
  - OS Version: Kali Linux 2024.3  

**Site B (Branch Office / Right Network)**  
- **pfSense B Firewall:** WAN – 10.10.10.2  |  LAN – 192.168.60.1  
- **Linux Mint (Client):** 192.168.60.10 (Static IP)  
  - Role: Primary client for VPN validation and connectivity testing  
  - OS Version: Linux Mint 21.3 (Victoria)  
- **Windows 10 (Client):** 192.168.60.11 (Static IP)  
  - Role: Secondary test machine for multi-OS VPN verification  
  - OS Version: Windows 10 Pro (Build 22H2)  

**Shared Virtual Network (WANNet)**  
- Acts as the simulated internet link between pfSense A and pfSense B  
- Subnet: 10.10.10.0/24  

---

## 🏗️ Implementation Summary  

### 🔹 Step 1: Site-to-Site VPN Configuration
- Configured **pfSense firewalls** for **Site A** and **Site B**  
- Assigned network interfaces and IP addresses:  
  - Site A → WAN: `192.168.1.18`, LAN: `192.168.50.1/24`  
  - Site B → WAN: `192.168.1.22`, LAN: `192.168.60.1/24`
- Established **IPsec Tunnel (Phase 1 & Phase 2)** using:
  - Encryption: **AES-256**
  - Hash: **SHA-256**
  - DH Group: **14**
  - Authentication: **Pre-Shared Key**
- Matched subnets and encryption settings on both ends to ensure successful negotiation.
  
Site A

<img width="940" height="587" alt="image" src="https://github.com/user-attachments/assets/1a3b51cd-36d5-4028-b25b-7e3a594b6707" />

---

Site B
<img width="940" height="717" alt="image" src="https://github.com/user-attachments/assets/7c59ff42-de6c-4993-a242-d2edb6e95c5b" />

---

Pfsense Site A: Wan 

<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/e9382851-6558-4b2b-a3c5-7ed5437e1c9c" />

---

Pfsense Site B: Wan 
<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/b964c636-d695-4a71-8864-0f37c46cdc0a" />

---

Tunnel 1
<img width="940" height="1076" alt="image" src="https://github.com/user-attachments/assets/0e74e0cf-6594-451a-96a5-1f033d02dfcd" />

---

<img width="940" height="1076" alt="image" src="https://github.com/user-attachments/assets/b2f709a8-04c9-4e56-a669-8a229a234d40" />

---

<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/fdaba21a-5b2f-41b2-8295-35bf8f95e231" />

---


Tunnel 2
<img width="940" height="523" alt="image" src="https://github.com/user-attachments/assets/a93a400f-ae31-46c6-8254-d34ba36632c9" />

---

<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/8876cfc2-eaa9-4297-8c4b-83ff4815736a" />

---

<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/4ff21af5-b879-420b-b894-b991f65e484f" />


---

### 🔹 Step 2: Firewall Rules
- Allowed **IPsec** and **LAN** traffic on both firewalls.  
- Added inbound and outbound rules to permit encrypted traffic through IPsec.  
- Verified connectivity between both LANs using `ping` and `tracert`.

On Site A: 

<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/c863297d-adc2-445b-a995-3395bd56309d" />

---

<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/59a5d25b-eecb-418d-93fb-f61b07d906e1" />

---

On Site B: 

<img width="940" height="527" alt="image" src="https://github.com/user-attachments/assets/489f5964-2c0d-452a-9a0d-6da21e44d586" />

---

<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/4b94d6a6-f8c1-4bf6-8022-4bf60dcd5249" />

---


Tunnel is established and its up 

<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/ea1cfe66-2bcc-4bd2-bbcb-eb2be531dd28" />

---

<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/00773d07-1084-44d0-9259-46100bbf894e" />



---

### 🔹 Step 3: Client Configuration
| Site | Devices | Operating Systems | IP Range |
|------|----------|-------------------|----------|
| **Site A** | Kali Linux, Ubuntu | 192.168.50.10–100 | Connected via pfSense A |
| **Site B** | Windows 10, Linux Mint | 192.168.60.10–100 | Connected via pfSense B |

- Each host was configured with static IPs and tested for secure communication.

Site A
Kali Linux

<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/6408a5ff-2332-43a2-9fbb-6ed52d8899da" />

Ubuntu

<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/56ea2574-9b1c-41fe-922d-9294bc896211" />

Site B

Windows 10

<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/2a90d5a8-6914-4323-b6a7-374dddaed0c8" />

Linux Mint

<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/048b82d4-f99d-4616-b51f-b365493bf4e1" />





---

### 🔹 Step 4: Data Transfer & Encryption Validation
- Conducted file transfer tests between Site A and Site B.  
- Captured traffic in **Wireshark** to verify end-to-end encryption — all packets were unreadable in plaintext.  
- Validated IPsec tunnel stability via **pfSense Status > IPsec** interface.

Sending file from Site A: 

<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/d22342fa-4545-4c1a-9df7-6df04b4467d8" />

Verifying it from site B: 

<img width="790" height="444" alt="image" src="https://github.com/user-attachments/assets/561e7ac7-5861-4a01-ad1b-985b45de3357" />

Site A&B: 
1.	Ipsec Tunnel encrypted with Strong pre shared key 
2.	It encryption algorithm is “AES” 256 bits and hash algorithm is “SHA 256”

<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/7bc7f563-e48f-4be8-8e48-aaf1e3180ab8" />

4.	Firewall rule for WAN interface
   
<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/d49f1e40-6d28-4ff4-bb3c-0727e5cb635e" />

6.	Ipsec rule for both site
   
<img width="940" height="526" alt="image" src="https://github.com/user-attachments/assets/9c4cf9c9-aa5c-4d6f-baba-15e8a3ac7d90" />

8.	Packet capture by “Wireshark”. We can see that the transfer data is encrypted.

<img width="940" height="527" alt="image" src="https://github.com/user-attachments/assets/62e39e16-6162-4381-bdd8-d9b31e08a120" />

<img width="940" height="528" alt="image" src="https://github.com/user-attachments/assets/2f4eb9bb-0b2b-425a-bb91-48ec34cfcff1" />

<img width="940" height="529" alt="image" src="https://github.com/user-attachments/assets/5db316fd-cf61-4100-9ebf-8011c999c35c" />


---

## 🌐 Network Topology 

<img width="940" height="374" alt="image" src="https://github.com/user-attachments/assets/0ce60633-c3ae-4af1-8a88-1e23a59ba36f" />

## 🏁 Conclusion  

The project successfully implemented a **secure Site-to-Site VPN** using **pfSense firewalls**, achieving encrypted inter-site communication and demonstrating real-world enterprise-level network security practices.  
It reinforced practical skills in **VPN deployment, encryption protocols, and firewall configuration** — essential for cybersecurity and network engineering roles.

---

## 📜 License  
This project is released under the **MIT License**.  
Feel free to use and modify for learning or academic purposes.




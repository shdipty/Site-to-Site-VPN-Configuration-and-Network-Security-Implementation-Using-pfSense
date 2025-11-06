============================================================
pfSense Site-to-Site VPN Network Security Implementation Guide
============================================================

Author: Shadia Rahman Dipty
Environment: Oracle VirtualBox (v7.1.2) | pfSense CE (v2.7.2)

============================================================
1️⃣ Objective
============================================================
To design, implement, and validate a secure site-to-site IPsec VPN
using pfSense firewalls between two virtual networks (Site A & Site B).
This setup simulates a real enterprise environment focused on
encrypted data communication, firewall security, and VPN configuration.

============================================================
2️⃣ Software and Versions
============================================================
• Oracle VirtualBox .................... v7.1.2
• pfSense CE ............................ v2.7.2 (ISO image)
• Wireshark ............................. v4.4.2
• Ubuntu Desktop (Client) ............... 24.04 LTS
• Kali Linux (Testing) .................. 2024.3
• Windows 10 Pro (Evaluation) ........... Build 22H2

============================================================
3️⃣ Hardware Configuration (Host)
============================================================
• OS: Windows 11 Home
• CPU: Intel i5 (11th Gen)
• RAM: 16 GB
• Storage: 512 GB SSD

============================================================
4️⃣ Network Topology
============================================================
We create two secure LANs connected via pfSense VPNs:

           Site A (192.168.50.0/24)
              |       LAN
           [pfSense A] === IPsec === [pfSense B]
              |       LAN
           Site B (192.168.60.0/24)

• pfSense A WAN: 10.10.10.1
• pfSense B WAN: 10.10.10.2
• pfSense A LAN: 192.168.50.1
• pfSense B LAN: 192.168.60.1

============================================================
5️⃣ Step-by-Step Installation
============================================================

Step 1: Create Internal Networks in VirtualBox
-----------------------------------------------
• Open VirtualBox → Tools → Network → Add “Internal Network”
  - WANNet (10.10.10.0/24)
  - SiteA-LAN (192.168.50.0/24)
  - SiteB-LAN (192.168.60.0/24)

Step 2: Create pfSense-A & pfSense-B VMs
----------------------------------------
• Each pfSense has two adapters:
  - Adapter 1: WAN (Internal Network: WANNet)
  - Adapter 2: LAN (Internal Network: SiteA-LAN or SiteB-LAN)
• Boot from pfSense ISO → Install pfSense normally.
• Assign interface IPs:
  - pfSense-A: WAN=10.10.10.1, LAN=192.168.50.1
  - pfSense-B: WAN=10.10.10.2, LAN=192.168.60.1

Step 3: Add Client VMs
-----------------------
• Site A → Ubuntu Desktop (192.168.50.10, GW=192.168.50.1)
• Site B → Windows 10 (192.168.60.10, GW=192.168.60.1)

Step 4: Enable Web Access
--------------------------
• From each client, access pfSense GUI at https://<LAN-IP>
  - Default user: admin / pfsense
  - Change password after login.

Step 5: Configure IPsec Tunnel (IKEv2)
--------------------------------------
On pfSense-A:
• VPN → IPsec → Add P1
  - Remote Gateway: 10.10.10.2
  - Authentication: Pre-Shared Key
  - PSK: vpn12345
  - AES-256, SHA-256, DH Group 14

Add Phase 2:
• Local Network: 192.168.50.0/24
• Remote Network: 192.168.60.0/24
• Save & Apply

Mirror configuration on pfSense-B with opposite IPs.

Step 6: Add Firewall Rules
---------------------------
• Firewall → Rules → IPsec → Add “Allow All” temporarily
• Firewall → Rules → LAN → Verify default “Allow LAN to any” exists

Step 7: Verify Tunnel
---------------------
• Status → IPsec → Should show “ESTABLISHED”
• If down, recheck PSK and subnets.

Step 8: Test Connectivity
-------------------------
• From Site A: ping 192.168.60.10
• From Site B: ping 192.168.50.10
• Successful ping = encrypted VPN working

Step 9: Validate Encryption
---------------------------
• Start Wireshark on WANNet adapter
• Capture ESP packets (filter: esp)
• You should NOT see plaintext packets (only encrypted traffic)

============================================================
6️⃣ Troubleshooting
============================================================
• If tunnel doesn’t establish, check:
  - Matching encryption settings on both pfSenses
  - Correct subnet definitions in Phase 2
  - Firewall rules allowing IPsec traffic

• If ping fails:
  - Check LAN firewall rules
  - Confirm default gateway and DNS

============================================================
7️⃣ Testing Results
============================================================
| Test | Expected Result | Status |
|------|------------------|---------|
| Tunnel Establishment | IPsec shows “Established” | ✅ Passed |
| Ping Connectivity | Sites A & B can communicate | ✅ Passed |
| Encrypted Packets | Wireshark shows ESP packets | ✅ Passed |

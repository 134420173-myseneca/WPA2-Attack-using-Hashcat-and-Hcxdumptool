# WPA2-Attack-using-Hashcat-and-Hcxdumptool
Introduction
WPA2 is the most used security protocol for securing wireless networks. Even with its robust encryption and security mechanisms, WPA2 is vulnerable to attacks, especially to those involving the handshake process. This report primarily focuses on two key tools used to attack the WPA2 secured network- hashcat and hcxdumptool, by exploiting the vulnerabilities in the handshake procedure. These tools enable threat actors to capture and crack the WPA2 passwords by applying various attack strategies such as dictionary and brute-force attacks.

Understanding WPA2 security
WPA2 utilizes Advanced Encryption Standard (AES) for encryption and Pre-Shared Key (PSK) for authentication. The WPA2 handshake is essentially a four-way process that builds a secure connection between the client and the access point which are also referred to as supplicant and authenticator respectively. However, the strength of the WPA2 encryption rely deeply on the strength of the pre-shared key.

WPA2 four-way handshake process
Step 1: The client sends a request to the access point (AP)
Step 2: The access point responds with its nonce (number used once)- a random value and message to start the handshake
Step 3: The client creates its own nonce along with the AP’s and derives a session key
Step 4: Both client and AP share the key information messages that confirms the establishment of a secure connection
At this stage, the handshake is completed and the keys for encryption are exchanged. The attackers try to capture this handshake essential for cracking the WPA2 password with the help of brute-force or dictionary attacks.



Tools for WPA2 attacks
Hashcat 
Hashcat is a powerful password cracking tool that can be used for a variety of hashing algorithms, including those used in WPA2. Hashcat utilizes the GPU (Graphics Processing Unit) to accelerate the cracking process, allowing for efficient brute-forcing or dictionary-based cracking of passwords.

WPA2 Handshake Process
When an attacker captures the WPA2 handshake, it holds the hash of WPA2 Pre-Shared Key (PSK) obtained from the passphrase. This hash can be cracked using hashcat to retrieve the original passphrase.
Most common attacks in Hashcat:

Brute-Force attack- Hashcat tries all possible combination of characters until it cracks the password.
Dictionary attack- The attacker attempts every possible password combination from a wordlist and matches the hash of the word from the wordlists with the captured hash.
Rule-based attack- Hashcat implies pre-defined rules to a dictionary by adding commonly used prefixes and suffixes or replacing alphabets with special characters to create an extensive list of passwords.

Hcxdumptool
Hcxdumptool is a tool used for capturing WPA2 handshake from wireless networks. As part of the hcxtools suite, it is designed to attack the WPA2 and WPA3 networks.

Key features of hcxdumptool:

Capture WPA2 handshakes- hcxdumptool captures the 4-way handshake while the client is attempting to connect with the access point.
 
De-authentication attacks- hcxdumptool sends de-authentication packets to force clients to reconnect to the access point, initiating a handshake capture.
 
Output Formats- This tool can save the captured handshake in various formats such as .pcapng, which can further be converted for use in hashcat. 


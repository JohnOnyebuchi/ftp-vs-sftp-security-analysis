FTP vs SFTP Security Analysis

A hands-on cybersecurity project demonstrating the security differences between File Transfer Protocol (FTP) and SSH File Transfer Protocol (SFTP) through network traffic capture and analysis using Wireshark.

📌 Project Overview

This project investigates the security risks associated with transmitting files over traditional FTP and demonstrates how SFTP addresses these risks through encryption.

The experiment involved configuring an FTP server and an SSH/SFTP server in Kali Linux, transferring a test file through both protocols, and capturing the resulting network traffic with Wireshark.

The captured traffic was then analyzed to determine what information could be exposed to an attacker monitoring the network.

🎯 Objectives

- Configure a basic FTP server using "vsftpd".
- Configure SFTP using OpenSSH.
- Transfer a test file using both FTP and SFTP.
- Capture network traffic using Wireshark.
- Demonstrate that FTP credentials and data can be transmitted in plaintext.
- Demonstrate that SFTP traffic is protected by SSH encryption.
- Compare the security characteristics of FTP and SFTP.
- Understand the importance of encryption for data in transit.

🧪 Lab Environment

Component| Details
Operating System| Kali Linux
Virtualization| VirtualBox
FTP Server| vsftpd
Secure File Transfer| OpenSSH / SFTP
Packet Analyzer| Wireshark
FTP Client| Linux FTP client
SFTP Client| OpenSSH SFTP client
Test Interface| Loopback ("lo")
FTP Port| TCP/21
SSH/SFTP Port| TCP/22

🛠️ Tools Used

- Kali Linux
- VirtualBox
- Wireshark
- vsftpd
- OpenSSH
- FTP
- SFTP

🔬 Methodology

1. FTP Environment Setup

A local FTP server was configured using "vsftpd".

A dedicated test account named "ftpstudent" was created, along with a sample file:

"testfile.txt"

The FTP server was configured to listen on TCP port 21.

2. FTP Traffic Capture

The FTP client connected to the local FTP server using:

"127.0.0.1"

Wireshark captured the traffic through the loopback interface.

The FTP session included authentication and file retrieval operations.

3. FTP Traffic Analysis

Wireshark analysis demonstrated that sensitive FTP information could be observed in plaintext.

The captured traffic exposed:

- FTP username
- FTP password
- FTP commands
- File retrieval request ("RETR")
- Transferred file contents

This demonstrates the confidentiality risk associated with traditional FTP.

4. SFTP Environment

SFTP was tested using OpenSSH.

The same "ftpstudent" account and test file were used to make the comparison consistent.

The file was transferred using:

sftp ftpstudent@127.0.0.1

5. SFTP Traffic Capture

Wireshark was used to capture the SFTP session on the loopback interface.

The captured communication was identified as SSH Version 2 (SSHv2) traffic.

Unlike the FTP capture, the SFTP session did not expose the username, password, commands, or test-file contents as readable plaintext.

📊 Results

FTP

The FTP capture demonstrated that sensitive information can be exposed during transmission.

Observed information included:

- "USER ftpstudent"
- "PASS"
- "RETR testfile.txt"
- Readable test-file content

SFTP

The SFTP capture showed:

- SSHv2 traffic
- Encrypted session data
- No readable FTP-style authentication commands
- No readable test-file contents in the captured traffic

A search for the known plaintext test-file content produced no matching packets in the SFTP capture.

🔐 FTP vs SFTP

Security Feature| FTP| SFTP
Encryption| ❌ No| ✅ Yes
Credentials protected| ❌ No| ✅ Yes
Commands protected| ❌ No| ✅ Yes
File contents protected| ❌ No| ✅ Yes
Common control port| TCP/21| TCP/22
Underlying security| None| SSH
Suitable for sensitive transfers| ❌| ✅

🧠 Security Analysis

The experiment demonstrates why traditional FTP should not be used for transmitting sensitive information across untrusted networks.

Because FTP does not encrypt its communication, an attacker capable of capturing network traffic may be able to recover authentication information and transferred data.

SFTP operates through the SSH protocol and protects the communication using encryption. This provides confidentiality for credentials, commands, and transferred data while also providing integrity protections through the SSH transport.

It is important to note that encryption does not make the connection invisible. Network observers may still identify that an SSH connection exists and observe metadata such as IP addresses, ports, timing, and packet sizes. However, the protected session contents are not exposed as plaintext.

🌍 Real-World Implications

Organizations frequently transfer sensitive information such as:

- Customer records
- Financial documents
- Configuration files
- Application backups
- Business reports
- Credentials and secrets

Using unencrypted FTP for such data can create serious confidentiality and security risks.

For secure file transfers, organizations should use encrypted alternatives such as SFTP or other appropriately secured file-transfer mechanisms.

📸 Evidence

The "screenshots/" directory contains evidence collected during the laboratory exercise.

Evidence includes:

- FTP server configuration
- Successful FTP authentication
- FTP packets captured in Wireshark
- Exposed FTP credentials
- FTP file retrieval request
- Readable FTP file contents
- Successful SFTP transfer
- SSHv2 traffic
- SFTP traffic where the test-file plaintext was not visible

📁 Project Structure

ftp-vs-sftp-security-analysis/
│
├── screenshots/
├── captures/
├── report/
├── docs/
└── README.md

🎓 Learning Outcomes

Through this project, I gained practical experience in:

- Network traffic capture
- Wireshark packet analysis
- FTP protocol analysis
- SSH/SFTP analysis
- Linux server configuration
- Authentication security
- Encryption in transit
- Identifying security weaknesses through packet analysis
- Documenting cybersecurity investigations

🚀 Future Improvements

Future versions of this project could include:

- A separate FTP client and server virtual machine
- Analysis of active and passive FTP modes
- Comparison of FTP, FTPS, and SFTP
- Network attack simulations in an isolated lab
- Additional Wireshark analysis
- Automated detection of insecure FTP authentication

⚠️ Disclaimer

This project was conducted in a controlled laboratory environment for educational and cybersecurity learning purposes.

No unauthorized systems or networks were targeted.

👤 Author

John Onyebuchi 

Cybersecurity Analyst

This project is part of my hands-on cybersecurity learning journey.

# 🛡️ SOC Analyst Training & Lab Notebook

Welcome to my training repository for **SOC Analyst**. Here I document my practical projects, network traffic analysis, SIEM operations, and threat research.

📌 **Live Lab Notebook (Notion):** [Click here to view my screenshots and detailed reports](https://spicy-clownfish-847.notion.site/SOC-Analyst-Lab-Notebook-3ef29add16b480cf915ec90482ca371d?source=copy_link)

---

## 🛠️ Tech Stack & Tools
* **Operating Systems:** Ubuntu Linux, Ubuntu Server, VirtualBox, SSH.
* **Learning Platform:** Cisco Networking Academy.
* **Networking & Analysis:** Wireshark, CLI Net-Tools.
* **Security & Labs:** OverTheWire, Wazuh, Splunk, MITRE ATT&CK.
* **Documentation & OPSEC:** GitHub, Notion.

---

## 📚 Phase 1: Essential Linux & Networking Commands (Cheatsheet)

### Network Diagnostics (Layer 3 & Layer 7)
| Command | Description | SOC Use Case |
| :--- | :--- | :--- |
| `ip a` | Displays interfaces and IP addresses | Identify local IP and active network interfaces |
| `ping -c 4 <IP>` | Sends ICMP Echo Request packets | Verify basic connectivity with a target host |
| `curl -I <URL>` | Fetches only HTTP/S response headers | Inspect web server responses without downloading the body |

### File Navigation & Manipulation
| Command | Description | SOC Use Case |
| :--- | :--- | :--- |
| `ls -la` | Lists all files, including hidden (`.`) | Detect malware or hidden scripts in directories |
| `cat ./-` | Reads a file whose name is a dash | Avoid interpreting the dash as a command flag |
| `cat "file name"`| Reads a file with spaces in the name | Analyze logs or files with non-standard naming conventions |

---

### Log Analysis & Forensic Search
| Command | Description | SOC Use Case |
| :--- | :--- | :--- |
| `file <file>` | Determines the actual file type (*magic bytes*) | Detect malicious artifacts camouflaged with fake extensions |
| `find <path> -size <bytes>` | Search by system attributes (size, permissions, user) | Locate suspicious or modified files on a compromised server |
| `grep "pattern" <file>` | Filters text lines that match a specific term | Identify IoCs, malicious IPs, or key events within raw logs |
| `2>/dev/null` | Redirects standard error output (STDERR) | Silence "permission denied" errors to reduce terminal noise |

---

### Data Manipulation & Payload Deobfuscation
| Command | Description | SOC Use Case |
| :--- | :--- | :--- |
| `sort file \| uniq -u` | Filters and displays only unique lines | Isolate anomalous single-occurrence log events |
| `strings <file>` | Extracts printable ASCII strings from binaries | Perform basic static analysis on suspicious executables |
| `base64 -d <file>` | Decodes Base64 encoded data | Deobfuscate encoded malicious payloads (e.g., PowerShell) |
| `tr 'A-Za-z' 'N-ZA-Mn-za-m'` | Translates characters using substitution | Reverse basic ROT13 obfuscation schemes |

---

### Advanced Payload Extraction & Network Services
| Command | Description | SOC Use Case |
| :--- | :--- | :--- |
| `xxd -r <file>` | Reverses a hex dump into a binary file | Reconstructing obfuscated malware payloads |
| `tar -xf <archive>` | Extracts files from a tar archive | Unpacking bundled malicious artifacts |
| `ssh -i <key> <user>@<IP>` | Authenticates using a private identity key | Pivoting across servers and identifying exposed credentials |
| `nc <host> <port>` | Reads/writes data across TCP/UDP connections | Interacting with open ports, banner grabbing, and testing C2 channels |

---

*Portfolio prototype in continuous development.*

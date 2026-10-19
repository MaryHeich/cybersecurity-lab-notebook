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

## 📚 Phase 1: Essential Linux & Networking Commands

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

## 📚 Phase 2: Network Traffic Analysis & Protocol Inspection

### Network Packet Analysis & Wireshark Display Filters
| Command / Filter | Description | SOC Use Case |
| :--- | :--- | :--- |
| `wireshark &` | Launches the Wireshark GUI packet analyzer in the background | Initiating live network interface capture and packet forensics |
| `http` | Display filter isolating unencrypted HTTP traffic | Detecting cleartext protocols, session IDs, and unencrypted credentials |
| `tls` or `ssl` | Display filter isolating TLS handshake packets | Analyzing secure traffic metadata (e.g., SNI) without breaking encryption |
| **Follow TCP Stream** | Reassembles a complete client-server TCP conversation | Reconstructing HTTP requests/responses, payload analysis, and inspecting cleartext headers/User-Agents |

---

### Command-Line Packet Analysis (Tshark)
| Command | Description | SOC Use Case |
| :--- | :--- | :--- |
| `tshark -i <interface> -c <num> -w <file>` | Captures a specific number of live packets to a PCAP file | Performing headless network packet capture on remote Linux servers |
| `tshark -r <file> -Y "<filter>"` | Reads a PCAP file and applies display filters | Offline forensic analysis and protocol filtering without a GUI |
| `tshark -r <file> -T fields -e <field>` | Extracts specific packet header fields in tabular format | Automated log parsing, IOC extraction, and rapid incident triage |

---

### TLS Traffic Analysis & Metadata Extraction
| Command / Filter | Description | SOC Use Case |
| :--- | :--- | :--- |
| `tls.handshake.type == 1` | Wireshark display filter for TLS `Client Hello` packets | Isolating initial session negotiation parameters and client capabilities |
| `tls.handshake.extensions_server_name` | Filter/Field targeting the Server Name Indication (SNI) | Extracting target domain names from encrypted HTTPS sessions |
| `tshark -r <file> -Y "tls.handshake.type == 1" -T fields -e tls.handshake.extensions_server_name` | Extracts requested SNI domains from a PCAP file via CLI | Automated threat hunting for malicious C2 domains in encrypted traffic |

---

### HTTP Traffic Analysis & Web Inspection
| Command / Filter | Description | SOC Use Case |
| :--- | :--- | :--- |
| `http.request.method == "GET"` | Wireshark display filter for HTTP GET requests | Isolating resource retrieval requests in web traffic captures |
| `http.response.code >= 400` | Filters HTTP responses returning client/server errors | Triaging directory brute-forcing, missing resources, or access denials |
| `tshark -r <file> -T fields -e http.request.uri -e http.user_agent` | Extracts requested URIs and User-Agent strings from PCAP | Rapid web log forensic parsing, IoC extraction, and threat hunting |

---

### Reconnaissance & Port Scanning Analysis
| Command / Filter | Description | SOC Use Case |
| :--- | :--- | :--- |
| `tcp.flags.syn == 1 && tcp.flags.ack == 0` | Wireshark filter for TCP SYN (Stealth) scan packets | Detecting half-open connection attempts and network footprinting |
| `tcp.flags.reset == 1` | Filters TCP RST flags | Analyzing connection teardowns, closed port responses, or firewall blocks |
| `tshark -r <file> -Y "tcp.flags.syn == 1 && tcp.flags.ack == 0" -T fields -e ip.src -e tcp.dstport` | Extracts scanning sources and targeted destination ports via CLI | Rapid IOC extraction and automated hunt for internal/external port mappers |

---

### Phase 3: Log Analysis & SIEM Fundamentals
#### Linux Log Analysis (`/var/log/auth.log`)
| Command / Pipeline | Description | SOC Use Case |
| :--- | :--- | :--- |
| `grep "Failed password" /var/log/auth.log` | Filters all failed authentication attempts in Linux | Identifying potential authentication anomalies and login failures |
| `grep "Failed password" /var/log/auth.log \| awk '{print $(NF-3)}' \| sort \| uniq -c \| sort -nr` | Aggregates and counts failed login attempts grouped by source IP | Detecting brute-force actors and IP-based credential attack patterns |

---

*Portfolio prototype in continuous development.*

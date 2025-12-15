# 🔒 Network Security Lab - DoS & Scanning Techniques

**Educational network security lab demonstrating network scanning and denial-of-service testing techniques on isolated lab environment.**

> *Learn network reconnaissance, vulnerability scanning, and DoS attack methods in a controlled educational setting.*

---

## ⚠️ DISCLAIMER

**This project is for EDUCATIONAL PURPOSES ONLY on isolated lab networks.**

- ✅ Use ONLY on networks you own or have explicit permission to test
- ✅ Use ONLY in isolated lab environments (Host-only network)
- ✅ Never use these techniques on production systems or networks you don't own
- ✅ Unauthorized network attacks are ILLEGAL

---

## 📚 Overview

This repository documents network security testing techniques using industry-standard tools. All exercises are performed on a controlled lab environment with Metasploitable2 virtual machine.

**Lab Environment:**
- **Target:** Metasploitable2 (local lab VM)
- **Network:** Host-only (isolated)
- **Purpose:** Educational DoS & network scanning practice
- **Location:** Birmingham, UK

---

## 🎯 Tools & Techniques Covered

### 1. **Nmap - Network Mapper**
- Basic network scanning
- SYN stealth scanning
- Timing templates
- Decoy scanning
- Host randomization

### 2. **Hping3 - Packet Crafting**
- TCP SYN flooding
- Flood mode testing
- Random source IP spoofing
- Port-specific targeting

---

## 📋 Lab Commands Explained

### Command 1: Basic Nmap Scan
```bash
nmap 192.168.56.101
```

**What it does:**
- Performs a basic network scan on target IP
- Discovers open ports
- Identifies running services
- Shows default port status

**Output includes:**
- Host status (up/down)
- Open ports
- Service names
- Service versions (if detected)

**Use case:** Initial reconnaissance, service discovery

---

### Command 2: SYN Stealth Scan with Timing
```bash
sudo nmap -sS -T2 192.168.56.101
```

**Flags explained:**
- `-sS` = SYN Stealth Scan (half-open connection)
- `-T2` = Paranoid timing (very slow, less detectable)

**What it does:**
- Sends SYN packets without completing TCP handshake
- Slower scanning to avoid detection
- More stealthy than basic scan
- Requires root privileges

**Advantages:**
- Less likely to trigger IDS/IPS alerts
- Doesn't create full connections
- Leaves fewer logs

**Use case:** Stealth reconnaissance, avoiding detection

---

### Command 3: Advanced Evasion Scan
```bash
sudo nmap -sS -T2 -f -D RND:5 --randomize-hosts 192.168.56.101
```

**Flags explained:**
- `-sS` = SYN Stealth Scan
- `-T2` = Paranoid timing (very slow)
- `-f` = Fragment packets (evade firewalls)
- `-D RND:5` = Use 5 random decoy IPs
- `--randomize-hosts` = Randomize host order

**What it does:**
- Fragments packets to bypass packet filters
- Sends decoy packets from random IPs
- Randomizes scan order
- Makes scan harder to detect and trace

**Advanced evasion techniques:**
- Packet fragmentation
- Decoy scanning
- Random host ordering
- Slow timing

**Use case:** Advanced evasion, testing IDS/IPS effectiveness

---

### Command 4: TCP SYN Flood Attack
```bash
sudo hping3 -S --flood --rand-source -p 80 192.168.56.101
```

**Flags explained:**
- `-S` = Set SYN flag
- `--flood` = Send packets as fast as possible
- `--rand-source` = Randomize source IP
- `-p 80` = Target port 80 (HTTP)

**What it does:**
- Sends massive number of SYN packets
- Uses random source IPs (spoofing)
- Targets port 80 (web server)
- Attempts to exhaust server resources

**Attack mechanism:**
- Server allocates resources for each SYN
- Server waits for ACK that never comes
- Connection table fills up
- Legitimate connections rejected

**Impact:**
- Denial of Service (DoS)
- Server becomes unresponsive
- Legitimate users cannot connect

**Use case:** DoS testing, understanding attack vectors

---

## 🔧 Lab Setup

### Prerequisites
- Kali Linux or similar penetration testing OS
- VirtualBox or VMware
- Metasploitable2 VM
- Host-only network configured
- Root/sudo access

### Installation

```bash
# Update system
sudo apt update && sudo apt upgrade -y

# Install nmap
sudo apt install nmap -y

# Install hping3
sudo apt install hping3 -y

# Verify installation
nmap --version
hping3 --version
```

### Network Configuration

```bash
# Check network interfaces
ip link show

# View host-only network
ip addr show

# Ping target to verify connectivity
ping 192.168.56.101
```

---

## 📊 Lab Exercises

### Exercise 1: Basic Reconnaissance
```bash
# Perform basic scan
nmap 192.168.56.101

# Analyze results:
# - Which ports are open?
# - What services are running?
# - What OS is detected?
```

### Exercise 2: Stealth Scanning
```bash
# Perform stealth scan
sudo nmap -sS -T2 192.168.56.101

# Compare with basic scan:
# - How long did it take?
# - Are results different?
# - Why use stealth scanning?
```

### Exercise 3: Evasion Techniques
```bash
# Perform advanced evasion scan
sudo nmap -sS -T2 -f -D RND:5 --randomize-hosts 192.168.56.101

# Analyze evasion:
# - How does fragmentation help?
# - Why use decoys?
# - What's the purpose of randomization?
```

### Exercise 4: DoS Testing
```bash
# WARNING: Only on lab environment!
# Send SYN flood
sudo hping3 -S --flood --rand-source -p 80 192.168.56.101

# Monitor impact:
# - Does target become unresponsive?
# - How many packets sent?
# - What's the CPU/memory impact?
```

---

## 🛡️ Defense Mechanisms

### Against Nmap Scanning
- **Firewall rules** - Block port scanning
- **IDS/IPS** - Detect scanning patterns
- **Rate limiting** - Limit connection attempts
- **Port knocking** - Hide services

### Against SYN Flood
- **SYN cookies** - Reduce memory usage
- **Rate limiting** - Limit SYN packets
- **Firewall rules** - Block suspicious traffic
- **Load balancing** - Distribute traffic

### Against Spoofing
- **Ingress filtering** - Block spoofed IPs
- **Egress filtering** - Prevent outgoing spoofed packets
- **BCP 38/RFC 2827** - Best practices

---

## 📈 Learning Outcomes

After completing this lab, you will understand:

✅ How network scanning works
✅ Difference between scan types
✅ Evasion techniques and their purpose
✅ DoS attack mechanisms
✅ Defense strategies
✅ Ethical and legal considerations
✅ Proper lab environment setup
✅ Network security fundamentals

---

## 🔗 Resources

### Tools Documentation
- [Nmap Official Guide](https://nmap.org/book/)
- [Hping3 Documentation](http://www.hping.org/)
- [Metasploitable2 Guide](https://docs.rapid7.com/metasploit/metasploitable-2/)

### Security Certifications
- CEH (Certified Ethical Hacker)
- OSCP (Offensive Security Certified Professional)
- CompTIA Security+
- GIAC Security Essentials (GSEC)

### Best Practices
- Always get written permission
- Use isolated lab environments
- Document all activities
- Follow responsible disclosure
- Understand legal implications

---

## ⚖️ Legal Notice

**IMPORTANT:**
- Unauthorized network attacks are ILLEGAL
- Violating computer fraud laws can result in criminal charges
- This lab is for EDUCATIONAL purposes ONLY
- Always obtain written permission before testing
- Use only on networks you own or have explicit authorization

---

## 📝 Lab Notes

### Observations
- Document scan results
- Note timing differences
- Record packet counts
- Analyze response patterns
- Compare evasion effectiveness

### Questions to Consider
- Why is stealth scanning slower?
- How do decoys help evade detection?
- What's the difference between scanning and attacking?
- How can defenders detect these techniques?
- What are the legal implications?

---

## 🎓 Next Steps

1. ✅ Complete all 4 exercises
2. ✅ Understand each command
3. ✅ Analyze results
4. ✅ Study defense mechanisms
5. ✅ Research ethical hacking
6. ✅ Pursue relevant certifications
7. ✅ Practice in lab environments
8. ✅ Learn responsible disclosure

---

## 🔗 Connect

- 💼 **LinkedIn:** [linkedin.com/in/george-miron](https://linkedin.com/in/george-miron)
- 📧 **Email:** mi.geo76@gmail.com
- 🐙 **GitHub:** [@georgemir](https://github.com/georgemir)
- 📍 **Location:** Birmingham, UK

---

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

<div align="center">

### ⚠️ Remember: With Great Power Comes Great Responsibility

*"Ethical hacking is about understanding security to build better defenses."*

**Use this knowledge responsibly and legally.**

</div>

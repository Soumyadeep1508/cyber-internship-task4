# cyber-internship-task4
Task 4 — Firewall Configuration and Port Blocking
**Elevate Labs — Cyber Security Internship**

---

## 📌 Objective
The objective of this task is to configure a firewall rule on a Windows system to block inbound network traffic on a specific port, test the rule, and verify that the firewall effectively prevents external connections.

---

## 🛠 Tools & Environment
- **Operating System:** Windows 10  
- **Firewall:** Windows Defender Firewall (Advanced Security)  
- **Testing Tools:** PowerShell, Netcat (`nc`)  
- **Network Type:** Local Wi-Fi Network  

---

## 🌐 System Information
- **Host IP Address:** `192.168.1.43`
- **Network Interface:** Wi-Fi
- **Blocked Port:** TCP 23 (Telnet)

---

## 🚀 Steps Performed

### 1️⃣ Verified Network Configuration
The system IP address was identified using: ipconfig- 192.168.1.43

2️⃣ Tested Port Accessibility Before Firewall Rule

A connection test was performed before applying any firewall rule:
Test-NetConnection -ComputerName 192.168.1.43 -Port 23 -InformationLevel Detailed
Result: TcpTestSucceeded : True
This confirmed that port 23 was reachable before firewall restrictions.

3️⃣ Created Firewall Rule to Block Port 23

An inbound firewall rule was created using PowerShell to block Telnet traffic:
New-NetFirewallRule `
  -DisplayName "Block Inbound Telnet (Port 23) - Task4" `
  -Direction Inbound `
  -LocalPort 23 `
  -Protocol TCP `
  -Action Block `
  -Profile Any
The rule was successfully added and enabled.

4️⃣ Tested Firewall Rule from a Different System

Due to Windows loopback and self-connection behavior, firewall validation was performed from another system on the same network.

Command executed from a different machine: nc -vz 192.168.1.43 23
Result: Connection timed out
This confirms that inbound traffic on port 23 was blocked by the firewall.

5️⃣ Cleanup
After verification, the firewall rule can be removed if required

📊 Results Summary
Test Scenario	                         Result
Before Firewall Rule	                 Port 23 Accessible
After Firewall Rule (Local Loopback)	 Allowed (Expected Behavior)
After Firewall Rule (External Test)	   Blocked (Connection Timed Out)

🧠 Key Observations

Windows Firewall does not block loopback (127.0.0.1) traffic.

Self-connection to the same host may bypass inbound filtering.

Firewall rules must be validated from external systems for accurate results.

Blocking Telnet improves security by preventing plaintext credential exposure.

🛡 Security Recommendation

Disable or block legacy services such as Telnet (TCP 23).

Regularly audit firewall rules.

Test firewall effectiveness from external sources.

Use secure alternatives such as SSH instead of Telnet.

📝 Conclusion

This task demonstrated practical firewall configuration, rule enforcement, and validation techniques. By blocking inbound Telnet traffic and verifying the block from an external system, the firewall was confirmed to be functioning as expected. This exercise reflects real-world defensive security practices used to reduce network attack surfaces.




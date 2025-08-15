# Villain Framework Reverse Shell — Lab Report

## 1. ⚙️ Setup Information

| Parameter | Value |
|-----------|-------|
| Payload Type | `windows/reverse_tcp/powershell` |
| LHOST | `192.168.56.101` *(Attacker VM — Host-Only IP)* |
| LPORT | `4444` |
| Target OS | Windows 10 Pro, Build 19045 |
| Attacker OS | Kali Linux 2024.2 |
| Network Type | Host-Only (VirtualBox) |
| Safety Measures | Isolated network, no internet access, benign payload, reverted to snapshot |

---

## 2. 🔁 Payload Delivery Method
The payload was transferred from the attacker VM to the victim VM using a Python HTTP server running in the attacker’s host-only network interface.  
The victim accessed the file via its browser and saved it locally.  
Execution was done manually in a PowerShell terminal on the victim VM.

---

## 3. 🖥️ Captured Host Information

| Collected Data | Value |
|----------------|-------|
| Hostname | `WIN10-VM` |
| IP Address | `192.168.56.105` |
| Logged-in User | `win10vm\\labuser` |
| OS Version | Microsoft Windows 10 Pro, Version 22H2 |

---

## 4. 🔎 Enumeration Performed
```powershell
whoami
ipconfig
systeminfo
echo "https://github.com/johndoe"
```
**Explanation:**
- `whoami` → Confirmed active user session.
- `ipconfig` → Verified network configuration within the host-only network.
- `systeminfo` → Retrieved OS version/build details.
- `echo` → Printed GitHub link as proof of execution.

---

## 5. 📊 Observations & Evidence
**Process Events (Sysmon Event ID 1)**  
- `powershell.exe` launched with the payload command line.  
- Parent process: `explorer.exe` (user-initiated execution).  

**Network Events (Sysmon Event ID 3)**  
- Outbound TCP connection from `192.168.56.105` (victim) to `192.168.56.101:4444` (attacker).  

**Packet Capture (Wireshark)**  
- 3-way TCP handshake observed.
- Payload data exchange followed immediately after connection establishment.

**Screenshots**  
- Villain interface showing active session.
- Sysmon logs showing process and network event correlation.
- Wireshark capture highlighting the reverse connection.

---

## 6. 🛡️ Detection Opportunities
- **Host-based:** Alert on `powershell.exe` spawning with encoded/obfuscated arguments.
- **Network-based:** Monitor for outbound connections from non-browser processes to non-standard ports.
- **Log Correlation:** Combine Sysmon process + network events to identify suspicious egress.

---

## 7. 🛠️ Prevention Measures
- Implement application allow-listing for PowerShell scripts.
- Restrict outbound traffic to known ports and hosts.
- Enable PowerShell Constrained Language Mode for standard users.
- Monitor and block execution of unsigned scripts from user directories.

---

## 8. 🔄 Cleanup & Reset
- Terminated Villain listener.
- Deleted payload from victim system.
- Verified no persistence mechanisms created.
- Restored VMs to pre-lab snapshot.

---

## 9. 📌 Reflection
This exercise demonstrated reverse-shell–style behavior in a controlled, isolated environment.  
The main takeaway is that reverse shells can bypass inbound firewall rules by initiating outbound connections from the victim.  
Proper detection requires both host-level and network-level monitoring, along with strict outbound traffic controls.

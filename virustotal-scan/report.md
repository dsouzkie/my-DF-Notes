# VirusTotal Analysis Report

## 📁 File Info
- Filename: malware_sample.zip
- File inside: malware_sample.docx
- Hashes:
  - MD5: f1fd4cf59c5cfb5e4ab5fd8570889fdb
  - SHA1:48543fec63c090153308892c3cdfc411979c4b45
  - SHA256: 
ae2a513b61febc225d5e374ab22dba754a3d38e49b7bbd442fe3f9bab16b8fb1 

## 🧪 Detection
| Engine       | Detection                          |
|--------------|------------------------------------|
| AhnLab-V3    | Malware/Win.Kryptik.C5784104        |
| Alibaba      | Trojan:MSIL/Taskun.cf3a01e2         |
| AliCloud     | Trojan:MSIL/Egairtigado.Gen         |
| ALYac        | Trojan.GenericKDZ.112786            |
| Arcabit      | Trojan.Generic.D1B892               |
| Arctic Wolf  | Unsafe                              |
| Avast        | Win32:MalwareX-gen [Pws]            |
| AVG          | Win32:MalwareX-gen [Pws]            |

## 📡 Network Indicators
api.telegram.org
dyndns.org
reallyfreegeoip.org

104.21.112.1
104.21.16.1
104.21.32.1
104.21.48.1
104.21.64.1
104.21.80.1
104.21.96.1
132.226.247.73
132.226.8.169
149.154.167.220

## 📊 Behavioral Summary
Behavioral Summary

Executes malicious payload (file.exe) from the user’s desktop.

Uses PowerShell commands (Add-MpPreference -ExclusionPath) to add Windows Defender exclusions, evading antivirus detection.

Creates and injects processes into legitimate executables (svchost.exe, updater.exe) to blend malicious activity with normal system processes.

Drops multiple files and scripts (.ps1, .psm1, .log) into temp folders and usage log directories, likely for execution and tracking.

Deletes temporary PowerShell policy test scripts to remove traces of execution.

Modifies registry keys under HKCU and HKLM for Explorer policies, AppID, and tracing settings—possibly for persistence and to alter system behavior.

Opens and modifies system files and cache databases in C:\ProgramData\Microsoft\Windows\Caches and AppRepository.

Establishes persistence mechanisms via registry changes and mutex creation.

Exfiltrates data via SMTP, using hardcoded credentials for mail.gaziotomasyon.com.tr (port 587).

Checks for analysis/debugging environments using functions like IsDebuggerPresent and GetSystemMetrics.

## 🗣️ Community Insight
Votes: 2 total → 1 malicious (-1), 1 harmless (-11).

Comments: 6 community comments present, discussing the sample’s behavior and confirming suspicion of malicious macros and payload download activity.

## 🔐 Public Link
https://www.virustotal.com/gui/file/ae2a513b61febc225d5e374ab22dba754a3d38e49b7bbd442fe3f9bab16b8fb1

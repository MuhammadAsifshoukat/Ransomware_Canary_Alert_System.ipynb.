# 🛡️ Automated Ransomware Decoy / Canary File Alert System

A **Blue Team / SOC / DFIR** project that detects ransomware-like behaviour using decoy ("canary") files, real-time file monitoring and a live SOC-style dashboard. Built in Google Colab with 100% free tools.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YOUR_USERNAME/ransomware-canary-alert-system/blob/main/Ransomware_Canary_Alert_System.ipynb)

> ⚠️ **Replace `YOUR_USERNAME`** in the badge link above with your GitHub username.

## 💡 Idea
Fake but tempting files (`Admin_Passwords_BACKUP.txt`, `Salary_Sheet_2026.xlsx`, `VPN_credentials_prod.txt`...) are hidden among real files. No legitimate user touches them, so **any activity on a canary is a high-confidence alert** (near-zero false positives).

## ✨ Features
| Module | Description |
|---|---|
| 🪤 Canary generator | 7 decoy files + 15 realistic dummy files, with SHA-256 and entropy baseline |
| 👁️ Real-time monitor | Python `watchdog` (inotify) file-event monitoring |
| 🧠 Detection engine | 4 layers: canary access/modify/rename/delete, mass file activity, Shannon entropy spike, suspicious extensions (`.locked`) |
| 🗺️ MITRE ATT&CK | Alerts mapped to T1486, T1485, T1083/T1005, T1027 |
| 📊 Live dashboard | Risk score, severity chart, timeline, live alerts (opens in a separate browser tab) |
| 🧪 Attack simulator | Safe, sandbox-only scenarios: fast burst, slow and stealthy, credential hunter |
| 📄 DFIR report | Timeline, SHA-256 before/after, entropy comparison, IOCs, recommendations |
| 📱 Optional alerts | Free Telegram bot notifications |

## 🧪 Scenarios
| Scenario | Behaviour | Detected by |
|---|---|---|
| 🔥 Fast burst | Overwrites and renames all files quickly | All rules |
| 🐢 Slow and stealthy | A few files with long gaps (below threshold) | **Canary only** (defence in depth) |
| 🕵️ Credential hunter | Only reads password/VPN decoys | `CANARY_ACCESSED` (early warning) |

## 🚀 How to run
1. Click the **Open in Colab** badge (or upload the `.ipynb` to [colab.research.google.com](https://colab.research.google.com)).
2. **Runtime → Run all**.
3. Click the dashboard link printed by the last code cell (opens in a new tab).
4. **▶ Start Monitor** → choose a scenario → **💥 Run Simulation** → view **🔬 Forensics** / **📄 Incident Report**.

## 📸 Screenshots
Add your screenshots to the `screenshots/` folder and reference them here:

```
![Dashboard](screenshots/dashboard.png)
```

## ⚠️ Safety and limitations
- The simulator only runs **inside the sandbox folder** (path guard) and uses **no real encryption** - it overwrites dummy files with random bytes.
- Containment (network isolation / process kill) is **simulated**.
- Process attribution is not implemented in Colab.

## 🔭 Future work
Sysmon/auditd process attribution, Wazuh SIEM integration, real EDR isolation, email alerts, multi-folder monitoring.

## 🧰 Tech stack
Python, watchdog, SQLite, HTML/CSS/JS dashboard, matplotlib, Google Colab.

## 👤 Author
**Muhammad Asif** - CS student aiming for SOC Analyst / DFIR roles.

*For educational and defensive security purposes only.*

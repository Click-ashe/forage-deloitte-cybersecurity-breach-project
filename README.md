![Project Banner] banner.png
# Deloitte Cybersecurity Web Activity Investigation (Daikibo)

This project is based on the Deloitte Forage Cybersecurity Virtual Experience. It simulates an investigation into a suspected data leak from Daikibo’s internal manufacturing status dashboard by analyzing web activity logs.

---

## 🎯 Objectives

- Determine whether an attacker could access the dashboard directly from the internet.
- Analyze web activity logs to identify suspicious user behavior.
- Identify the user ID most likely responsible for the data leak.
- Document findings in a SOC-style incident report.

---

## 📁 Project Structure

- `web_requests_sample.log` — Sample web activity data from Daikibo’s telemetry dashboard.
- `analysis-notes.md` — Step-by-step reasoning and observations during log review.
- `incident-report.md` — Final SOC-style incident report with conclusions and recommendations.
- `timeline.md` — Chronological sequence of key events from the logs.

---

## 🧠 Key Findings

- All IP addresses in the logs are internal (`192.168.x.x`), indicating the dashboard is only accessible via Daikibo’s intranet or VPN.
- There is **no evidence** of direct access from the public internet.
- Most users show normal, human-like browsing behavior (login → dashboard → occasional API calls).
- One user account, **`1FtyZHWX9c8JJTZiYqq4Bs`**, shows suspicious, automation-like API usage from IP `192.168.0.73`.

---

## 🚨 Suspicious Activity Summary

- **User ID:** `1FtyZHWX9c8JJTZiYqq4Bs`  
- **IP Address:** `192.168.0.73`  
- **Behavior:**
  - Rapid, structured API calls to `/api/factory/status` and `/api/factory/machine/status`.
  - Systematic enumeration of machines in multiple factories (`meiyo`, `berlin`).
  - Timing patterns consistent with scripted automation rather than human interaction.

---

## 🔒 Conclusions

- **External access:**  
  A hacker cannot access Daikibo’s manufacturing status dashboard directly from the internet. All requests originate from internal IP addresses, and the dashboard resides on the intranet.

- **Most suspicious user:**  
  The user ID with the most suspicious activity is **`1FtyZHWX9c8JJTZiYqq4Bs`**, whose session appears to have been used to systematically query machine status data via the API.

---

## 🛠 Skills Demonstrated

- Web log analysis
- Detection of automated vs human behavior
- Internal vs external threat reasoning
- Incident documentation and reporting
- Cybersecurity investigation mindset (SOC-style workflow)

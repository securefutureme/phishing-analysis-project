# Phishing mail analysis project

### Introduction
This repository contains short, practical analyses of **real** (and some fictional, sourced from various places) phishing emails. The ability to spot red flags and verify authenticity is crucial because:

- For end-users, it helps avoid clicks and stops incidents at the source — where many security breaches actually begin.
- For Helpdesk/SOC, it enables faster triage and escalation (domain/IP blocking, IOCs for SIEM), reducing response time.
- For administrators/cybersecurity teams, it provides a foundation for hard controls (DMARC, filtering, macros, one-click reporting).
- For leadership, it offers clear recommendations that reduce risk and cost (fraud, downtime, penalties).

**This repo is intended for:**
- **Users** — how to recognize phishing and what **not** to do.
- **SOC/IT** — an example structure for documenting phishing analysis.
- **Organizations** — training purposes.

| Analysis name | PL | ENG |
|---|---|---|
| UPS - phishing campaing | [Mail 1](documentation/email-01-PL.md) | [Mail 1](documentation/email-01-ENG.md) |
|  | [Mail 2](documentation/email-02-PL.md) | [Mail 1](documentation/email-02-ENG.md) |
|  | [Mail 3](documentation/email-03-PL.md) | [Mail 1](documentation/email-03-ENG.md) |
|  | [Mail 4](documentation/email-04-PL.md) | [Mail 1](documentation/email-04-ENG.md) |
|  | [Mail 5](documentation/email-05-PL.md) | [Mail 1](documentation/email-05-ENG.md) |

---

### What is phishing?
Phishing is a social-engineering technique where an attacker **impersonates** a person or organization to **steal sensitive data, infect devices, or perform other harmful actions.**

#### Examples of phishing:

- **Spear phishing** — a targeted email to a specific person/team using OSINT details (“Hi Kasia from HR…”) with a link/attachment to steal credentials or deliver malware.
- **Vishing** — voice phishing; phone scams impersonating trusted institutions (banks, police) or individuals to extract personal data.
- **Smishing** — SMS phishing; a text with a link to a fake page, e.g., payment/tracking gateway or “extra fee: 3.99 PLN”.
- **Whaling / CEO Fraud** — targeting executives (CEO/CFO); “from the boss” requesting urgent transfers or sensitive data.
- **BEC — Business Email Compromise** — a compromised legitimate mailbox of a company/partner; bank accounts swapped on invoices, “payment details update”, etc.
- **SEO poisoning / Search Engine Phishing** — malicious sites boosted in search (often via ads); users click “download Teams/Bank” and land on a clone.
- **Clone phishing** — replicating legitimate emails from trusted brands to coax victims into revealing sensitive info.
- **QR phishing (QRishing)** — a malicious QR code in an email/flyer leading to a fake login page or attacker site.
- **Consent/OAuth phishing** — instead of a password, asks you to “Grant access” to a purported app; in reality you hand over tokens.
- **MFA fatigue** — “bombarding” a victim with MFA push prompts until they accept one “by accident”.
- **Tech support / angler phishing** — fake “support” chats/ads (often on social media) prompting installation of remote tools.
- **Pharming/Wi-Fi captive hijack** — redirecting to a fake site (via DNS/hosts tampering) that looks identical to the real one to harvest credentials.
- **Watering hole** — compromising a frequently visited site (e.g., industry portal) to capture logins or plant malware.

---

### What you'll find
- case-by-case comprehensive analysis (`documentation/`),
- email content and headers (`analysis/`),
- screenshots (`screenshots/`),

**Workflow:**  
VM --> export phishing emails --> export content/headers --> analysis by schema --> tools to assess IPs and links --> **IOC Table**

---

### INFO
- **Some data (e.g., my email address) has been removed for privacy reasons.**
- **This project demonstrates my phishing-email analysis skills after completing the “Szkoła Security” course.**

---


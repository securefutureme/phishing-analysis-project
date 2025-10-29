
<details>
  <summary><b>🇵🇱 Polski — kliknij, by rozwinąć</b></summary>

<p>

# Projekt - Analiza maila phishingowego 

### Wstęp
W tym repo prezentuję krótkie, praktyczne analizy **realnych** (oraz fikcyjnych, zaczerpniętych z różnych źródeł) maili phishingowych. Umiejętność rozpoznawania czerwonych flag i weryfikacji autentyczności jest kluczowa, ponieważ:

- Użytkownikom pozwala nie kliknąć i zatrzymać incydent u źródła. Wbrew pozorom to właśnie tutaj powstaje najwięcej incydentów naruszających bezpieczeństwo.
- Helpdesk/SOC ułatwia szybką triage i eskalację (blokady domen/IP, IOC do SIEM), co skraca czas reakcji.
- Admnistratorom/cybersecurity daje podstawę do twardych kontroli (DMARC, filtrowanie, makra, zgłaszanie jednym kliknięciem).
- Kadrze kierowniczej zapewnia jasne rekomendacje ograniczające ryzyko i koszty (fraud, przestoje, kary).

**Adresuję moje repo do:**
- użytkowników – jak rozpoznać phishing i czego nie robić;
- SOC/IT – jako przykładowy sposób opisywania analizy phishingu;
- organizacji – w celach szkoleniowych;

#### Spis analiz

| Nazwa analizy | PL | ENG |
|---|---|---|
| Kampania phishingowa - UPS | [Mail 1](documentation/email-01-PL.md) | [Mail 1](documentation/email-01-ENG.md) |
|  | [Mail 2](documentation/email-02-PL.md) | [Mail 1](documentation/email-02-ENG.md) |
|  | [Mail 3](documentation/email-03-PL.md) | [Mail 1](documentation/email-03-ENG.md) |
|  | [Mail 4](documentation/email-04-PL.md) | [Mail 1](documentation/email-04-ENG.md) |
|  | [Mail 5](documentation/email-05-PL.md) | [Mail 1](documentation/email-05-ENG.md) |

---

### Co to jest phishing?
Phishing jest to metoda oszustwa opierająca się na **„podszywaniu”** się pod inną osobę albo instytucję, próbując w ten sposób **wyłudzić poufne dane, zainfekować komputer czy inne nieprzyjazne działania.**

#### Przykłady phishingu:

- **Spear phishing** — celowany mail do konkretnej osoby/zespołu, z detalami z OSINT („Cześć Kasiu, z HR…”) i linkiem/załącznikiem do kradzieży haseł lub malware.
- **Vishing** — voice phishing; oszustwo telefoniczne, w którym przestępcy podszywają się pod zaufane instytucje (np. banki, policję) lub osoby, aby wyłudzić poufne dane.
- **Smishing** — SMS phishing; SMS z linkiem do fałszywej wiadomości, np. bramki płatności/śledzenia paczki lub „dopłaty 3,99 zł”.
- **Whaling / CEO Fraud** — atak na kadrę (CEO/CFO); mail „od prezesa” z prośbą o pilny przelew lub poufne dane.
- **BEC — Business Email Compromise** — przejęta prawdziwa skrzynka firmy/partnera; zamiana numerów kont na fakturach, „aktualizacja danych płatności” itp.
- **SEO poisoning / Search Engine Phishing** — złośliwe strony wypchnięte wysoko w Google (często reklamy); użytkownik klika „pobierz Teams/Bank” i trafia na podróbkę.
- **Clone phishing** — imitowanie legalnych wiadomości e-mail od zaufanych firm w celu nakłonienia ofiar do ujawnienia poufnych informacji.
- **QR phishing (QRishing)** — złośliwy kod QR w mailu/ulotce prowadzący do fałszywej strony logowania lub strony atakującego.
- **Consent/OAuth phishing** — zamiast hasła prosi o „Zgódź się na dostęp” dla rzekomej aplikacji; w rzeczywistości oddajesz tokeny do konta.
- **MFA fatigue** — technika „bombardowania” push'ami MFA do ofiary, aż zaakceptuje „przypadkowo”.
- **Tech support / angler phishing** — fałszywy czat/ogłoszenie „pomocy technicznej” (często w social media), namawia do instalacji narzędzi zdalnych.
- **Pharming/Wi-Fi captive hijack** — przekierowanie na fałszywą stronę (np. manipulacja DNS/hosts), identyczną jak legalna, by wyłudzić dane.
- **Watering hole** — zainfekowanie często odwiedzanej strony (np. branżowy portal), by złowić loginy/zainfekować malware.

---

### Co znajdziesz
- rozszerzoną analizę case-by-case (`documentation/`),
- treści i nagłówki maila (`analysis/`),
- zrzuty ekranu (`screenshots/`),

**Workflow:**  
VM → eksport maili phishingowych → eksport treści/nagłówków → analiza wedle schematu → toole analizujące adresy IP i linki → **Tabela IOC**

---

### INFO
- **Niektóre dane, jak mój adres mailowy i inne zostały usunięte, z powodów prywatnych.**
- **Ten projekt jest ćwiczeniem obrazującym moje umiejętności analizy maila phishingowego po odbyciu kursu Szkoła Security.**

---</p>

</details>

<details>
  <summary><b>🇬🇧 English — click to expand</b></summary>

<p>

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

---</p>

</details>


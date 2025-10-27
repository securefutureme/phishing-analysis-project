# Mail 02 / Malware-Threat-Anlaysis phishing example

## 1) Podsumowanie

- **Motyw:** 
- **Typ ataku:** 
- **Skutek po kliknięciu:** 
- **Ocena końcowa:** 🟥 Phishing / 🟧 Podejrzane / 🟩 Legit

---
## 2) Opis analizy


---
##3) **Artefakty**

- **Treść:** [`analysis/body1.txt`](../analysis/body1.txt)
- **Nagłówki:** [`analysis/headers1.txt`](../analysis/headers1.txt)
- **Zrzuty ekranu:** [`/screenshots`](../screenshots)
- **Linki**:


## 3) Czerwone flagi

| Gdzie? | Obserwacje | Wniosek |
|---|---|---|
| Domena linku |  |  |
| Treść |  | Socjotechnika |
| Styl/HTML |  | |
| Stopka |  | |

---

## 4) Analiza nagłówków (jeśli dostępne)
| Pole | Wartość (zanonimizowana) | Notatka |
|---|---|---|
| `From` |  | np. Nie pasuje do marki |
| `Reply-To` | … | np. Inna domena niż `From` |
| `Return-Path` | … | np. Często domena faktycznej wysyłki |
| `Received` (ostatni hop) |  | np. Geolokacja/ASN odbiega od oczekiwanej |
| **SPF** |  |  |
| **DKIM** |  | jw. |
| **DMARC** |  | jw. |

## 5) Analiza URL
urlscan.io →
VirusTotal (URL) → 
WHOIS (who.is) →
MXToolbox → 
PhishTank → 

## 6) Tabela IOC

| Type        | Value                                           | Context                                   | First Seen  | Confidence |
|-------------|--------------------------------------------------|--------------------------------------------|-------------|-----------|
| Domain      |                               |         |             | High      |
| URL         |  |   |             | High      |
| Subject     |                       |                              |             | Medium    |
| Phrase      |                 |            |             | Medium    |
| IP          |                                                 |         |             | Low       |
| Email       |                                                 |                     |             | Low       |

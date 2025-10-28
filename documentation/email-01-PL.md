# Email 01 / UPS threat in private mail 

<p align="center">
  <img src="screenshots/mail1/header1.png" width="600" alt="Widok maila">
</p>

![Widok maila](screenshots/mail1/header1.png)

| Gdzie? | Obserwacje | Wniosek |
|---|---|---|
| Domena linku |  |  |
| Treść |  | Socjotechnika |
| Styl/HTML |  | |
| Stopka |  | |

| Pole | Wartość | Notatka |
|---|---|---|
| `From` |  | np. Nie pasuje do marki |
| `Reply-To` | … | np. Inna domena niż `From` |
| `Return-Path` | … | np. Często domena faktycznej wysyłki |
| `Received` (ostatni hop) |  | np. Geolokacja/ASN odbiega od oczekiwanej |
| **SPF** |  |  |
| **DKIM** |  | jw. |
| **DMARC** |  | jw. |

## Analiza URL

urlscan.io →

VirusTotal (URL) → 

WHOIS (who.is) →

MXToolbox → 

PhishTank → 

## Tabela IOC

| Type        | Value                                           | Context                                   | First Seen  | Confidence |
|-------------|--------------------------------------------------|--------------------------------------------|-------------|-----------|
| Domain      |                               |         |             | High      |
| URL         |  |   |             | High      |
| Subject     |                       |                              |             | Medium    |
| Phrase      |                 |            |             | Medium    |
| IP          |                                                 |         |             | Low       |
| Email       |                                                 |                     |             | Low       |

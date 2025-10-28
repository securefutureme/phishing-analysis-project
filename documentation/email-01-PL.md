# Email 01 / UPS threat in private mail 

Już na etapie wstępnego oglądu — z perspektywy zwykłego odbiorcy — w oczy od razu wpadają dwa elementy: alarmistyczny tytuł „Nie ma już czasu” oraz deklarowany nadawca „UPS”. 
To połączenie samo w sobie uruchamia intuicyjny hamulec: komunikat o skrajnym pośpiechu zwykle nie pasuje do typowego, spokojnego stylu komunikacji firm kurierskich.

**- UPS nie używa komunikatów w stylu „nie ma już czasu”; raczej „Twoja przesyłka czeka na odbiór”, „Twoja przesyłka jest w drodze” itp.**

**- Nie korzystałem ostatnio z usług kuriera UPS (brak kontekstu do takiej wiadomości).**

<p align="center">
  <a href="screenshots/mail1/header1.png">
    <img src="/screenshots/mail1/header2.png" width="600" alt="Widok maila (nagłówek)">
  </a>
</p>
<p align="center">
  <em>Rys. 1 — Podgląd początku wiadomości</em>
</p>

Po wejściu głębiej — podgląd wiadomości w preview w sandboxie — mail od razu przypomina klasyczny phishing. **W głównej mierze dlatego, że jest bardzo słabo wykonany.**
W treści nie widać żadnych elementów potwierdzających, że to faktycznie UPS (brak spójnej domeny nadawcy, brak identyfikatorów przesyłki). 
Pierwszy nagłówek **FROM**, potwierdza klasyczny przypadek podrobienia wyświetlanej nazwy i podszywania się pod znaną firmę **(Brand impersonation)**. 

Szybka inspekcja zawartości i osadzonych linków (po otwarciu wiadomości w formacie .txt) wskazuje na próbę wyłudzenia: **widoczny odnośnik „U.n.s.u.b” prowadzi bezpośrednio na adres IP 5[.]231[.]202[.]248,** a w kodzie umieszczono piksel śledzący z domeny chipcrack[.]net — obie wartości nie mają żadnego związku z domeną UPS. Rozjazd domeny względem marki oraz użycie surowego adresu IP w odnośniku CTA to klasyczne czerwone flagi kampanii masowych.









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

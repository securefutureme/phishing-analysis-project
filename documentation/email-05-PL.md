# Email 02 - 


## Podsumowanie

- **Motyw:** przekierowanie do strony kampanii (prawd. wyłudzenie danych/opłaty - nie można zweryfikować ze względu na wygaszoną kampapanię).
- **Typ ataku:** Prawdopodobnie masowy phishing z podrobieniem marki oraz metoda podrabiania wyświetlanej nazwy;
- **Ocena końcowa:** _**Phishing**_

| Gdzie?            | Obserwacje                                                                                                      | Wniosek |
|---                |---                                                                                                               |---|
| Nadawca (From)    | `"UPS"` <…@chipcrack[.]es>                                                                                       | **Metoda na podrabianie wyświetlanej nazwy** |
| Return-Path/DKIM  | `Return-Path: …@chipcrack[.]es`, `DKIM d=chipcrack[.]es (rsa-sha1)`                                              | Podpis atakującego, nie marki; DKIM nie uwiarygadnia UPS |
| Łańcuch Received  | `from aaa.altnewlywed[.]shop `                                                                                   | Wysyłka z losowej domeny, nie infrastruktury UPS |
| Domena linku (CTA)| `hxxp://5[.]231[.]202[.]248/...`                                                                               | **IP "surowy"** oraz **niezgodność domeny odbiorcy z marką** |
| Treść             | „**nie ma już czasu**”                                                                                         | **Socjotechnika** - alarminzm, wywołanie pośpiechu |
| Styl/HTML         | Tabelkowy szablon, klasy generatora, zewnętrzne proxy dla logo                                                | Niska jakość maila, brak spójności z marką |
| Grafiki           | Obraz z `i.imgur[.]com`                                                                                      | Assety hostowane poza marką - nietypowe dla UPS, plus nieaktywny obraz |
| Stopka            | „Unsub” IP `5[.]231[.]202[.]248`; oraz piksel `chipcrack[.]net/track/...`                                    | Link **nie** prowadzi do UPS; tracking kampanii |

### Analiza URL

##### urlscan.io
**hxxp://chipcrack[.]net/track/.../30285o9**
- To piksel śledzący otwarcie osadzony w phishu (ścieżka /track/... + 1×1 PNG). Służy to do potwierdzania, czy skrzynka jest „żywa” i mail został wyświetlony. Jest wykorzystwany do śledzenia kampani (ID w ścieżce), potencjalnie do dalszego spamowania.

**5[.]231[.]202[.]248**
- Skan zwraca błąd (We could not scan this website!). Prawdodobnie link już nie działa prawidłowo, ponieważ prawdopodobnie link już nie działa prawidłowo, ponieważ kampania została wygaszona lub serwer IP przestał odpowiadać / blokuje skanery.

##### VirusTotal 
<div align="center">
  <img src="/screenshots/mail1/virustotal.png" alt="Widok HTML" width="105%">
</div>
<p align="center"><em>Rys. 4 - Skan Virustotal</em></p>

##### WHOIS 
**5[.]231[.]202[.]248**
- RIPE region (RIPE NCC). Szczegóły właściciela do pobrania z bazy RIPE (RDAP). Adres nie należy do UPS. Pawdopodobnie serwer pośredni/VPS użyty w kampanii.

##### MXToolbox 
- wedle raportu mozemy wywnioskować że domena ma niską higienę pocztową i nie wygląda na oficjalny kanał wysyłki UPS - brak DMARC, brak/niepoprawny SPF oraz problemy z rekordami MX/DNS.
<div align="center">
  <img src="/screenshots/mail1/mxtoolbox.png" alt="Widok HTML" width="105%">
</div>
<p align="center"><em>Rys. 5 - Skan MXToolBox</em></p>


### Analiza nagłówków

| Pole                      | Wartość                                                                           | Notatka |
|---                        |---                                                                                  |---|
| `From`                    | `"UPS"` <…@chipcrack[.]es>                                                          | **Metoda na podrabianie wyświetlanej nazwy** |
| `Reply-To`                | —                                                                                    | n/a |
| `Return-Path`            | <…@chipcrack[.]es>                                                                    | Adres zwrotny wskazuje na domenę nadawcy kampanii. |
| `Received` (ostatni hop) | from aaa.altnewlywed[.]shop ([163.172.189.190])                                       | Ostatni host to VPS (Virtual Private Server) z obcą domeną; brak powiązania z UPS. |
| **SPF**                   | n/a                                                                                  | n/a |
| **DKIM**                  | `d=chipcrack[.]es; a=rsa-sha1; s=smtp`                                               | Podpis dla domeny atakującego, nie UPS |
| **DMARC**                 | n/a                                                                                  | n/a |


### Tabela IOC

| **Type**   | **Value**                                                                                              | **Context**                              | **Confidence** |
|---     |---                                                                                                        |---                                         |---|
| **Domain** | chipcrack[.]es                                                                                        | Envelope-From / Return-Path / DKIM d=     | High      |
| **Domain** | aaa[.]altnewlywed[.]shop                                                                              | Host nadawczy w `Received`                | High      |
| **IP**     | 163[.]172[.]189[.]190                                                                                 | Źródłowe IP serwera nadawcy               | High      |
| **URL**    | hxxp://5[.]231[.]202[.]248/ShpVWA32333Tpuf133gwzwgzcmey1491.../3028529                                | CTA/„U.n.s.u.b” z maila                    | High      |
| **Domain** | chipcrack[.]net                                                                                       | Tracker/piksel kampanii                    | Medium    |
| **URL**    | hxxp://chipcrack[.]net/track/3zpkFh32333PFCr133uvidiswzhm1491.../30285o9                              | Tracker/piksel kampanii                    | Medium    |
| **Subject**| „nie ma już czasu”                                                                                    | Wywołanie presji czasu (socjotechnika)      | Medium    |
| **Phrase** | „If you no longer wish to receive emails from us, please U.n.s.u.b”                                   | Frazy kampani                           | Medium    |

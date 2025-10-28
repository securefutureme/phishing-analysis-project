# Email 01 - UPS 

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
  <em>Rys. 1 — Nagłówki</em>
</p>

Po wejściu głębiej — podgląd wiadomości w preview w sandboxie — mail od razu przypomina klasyczny phishing. **W głównej mierze dlatego, że jest bardzo słabo wykonany.**
W treści nie widać żadnych elementów potwierdzających, że to faktycznie UPS (brak spójnej domeny nadawcy, brak identyfikatorów przesyłki). 
Pierwszy nagłówek **FROM**, potwierdza klasyczny przypadek podrobienia wyświetlanej nazwy i podszywania się pod znaną firmę **(Brand impersonation)**. 

Szybka inspekcja zawartości i osadzonych linków (po otwarciu wiadomości w formacie .txt) wskazuje na próbę wyłudzenia: **widoczny odnośnik „U.n.s.u.b” prowadzi bezpośrednio na adres IP 5[.]231[.]202[.]248,** a w kodzie umieszczono piksel śledzący z domeny chipcrack[.]net — obie wartości nie mają żadnego związku z domeną UPS. Rozjazd domeny względem marki oraz użycie surowego adresu IP w odnośniku CTA to klasyczne czerwone flagi kampanii masowych.

<div align="center">
  <img src="/screenshots/mail1/message1.png" alt="Podgląd wiadomości" width="35%">
  &nbsp;&nbsp;
  <img src="/screenshots/mail1/screenbody1.png" alt="Widok HTML" width="55%">
</div>
<p align="center"><em>Rys. 2,3 — Podgląd wiadomości + HTML</em></p>

Przy dalszej analizie maila, możemy zaobserować, że to nie jest korespondencja UPS, tylko kampania masowa z własnej infrastruktury atakującego. Pierwsza czerwona flaga, oprócz podrobienia wyświetlanej nazwy, to **Return-Path: <…@chipcrack.es>** — zwrotny adres także wskazuje na chipcrack.es. Ekstremalnie długi „local-part” (ciąg cyfr/liter) wygląda jak znacznik śledzący/identyfikator kampanii (VERP/track ID).

Następnie patrzymy na nagłówek **Received: from aaa[.]altnewlywed[.]shop ([163[.]172[.]189[.]190]).** Tu widzimy, że wiadomość weszła z hosta aaa.altnewlywed.shop na publicznym IP 163[.]172[.]189[.]190. To wygląda jak zwykły VPS serwer z losową domeną, więc to na pewno nie infrastruktura UPS. 

W dalszej analizie przystąpiłem do weryfikacji DKIM i SPF. Podpisy są wystawione dla chipcrack.es (nie ups.com - co jest kolejnym dowodem na phishing) i dodatkowo używają SHA-1 (słaby algorytm i przestarzały). Podpis DKIM dla domeny atakującego nie potwierdza autentyczności rzekomej marki — co najwyżej, że nadawca kontroluje chipcrack.es. **W całym mailu brakuje jednak SPF/DKIM/DMARC od serwera odbiorcy - czyli brakuje sekcji Authentication-Results.**. Jednak jest to też normalne działanie - bramy AV/antyspam czasem stripują lub zamieniają Authentication-Results: na swoje X-*. Mailing listy też potrafią zostawić tylko swoje metadane. Możliwe też, że stare systemy mailngowe w ogóle nie uruchamiają modułów SPF/DKIM/DMARC albo nie loguje wyników w Authentication-Results.

Z innych ciekawych wniosków, możemy zaobserwować, że w środku maila znajduje się link do obrazka na imgur.com. Niestety, po otworzeniu obrazka, nie znajdujemy go nawet na serwerze, co dodatkowo podważa wiarygodność wiadomości. Legalny nadawca (np. UPS) **raczej nie hostuje elementów maila na publicznym serwisie typu imgur.com — używa do tego własnej domeny.** Brak pliku sugeruje „jednorazową” kampanię (rotacja/wyczyszczenie zasobów, usunięcie przez Imgur lub autora), co jest typowe dla masowych phishingów: niechlujnie sklejony szablon, zewnętrzne hosty, krótki czas życia dowodów.

Nie możemy więc oficjalnie zacytować werdyktu, ale jest to bez znaczenia dla marki. Nadawca nie wysyła z domen UPS, więc żaden poprawny wynik nie uwiarygadnia „UPS” w polu From. Bramy AV/antyspam (gateway, DLP, MTA pośredni) czasem stripują lub zamieniają Authentication-Results: na swoje X-*. Forwardery/mailing listy też potrafią zostawić tylko swoje metadane.
Dalsze wyniki w urlscanio, whois, i mxtoolbox potwierdzają, że była to "masówka" phishingowa, która była wykonana jakiś czas temu.

## Podsumowanie

- **Motyw:** przekierowanie do strony kampanii (prawd. wyłudzenie danych/opłaty - nie można zweryfikować ze względu na wygaszoną kampapanię).
- **Typ ataku:** Prawdopodobnie masowy phishing z podrobieniem marki oraz metoda podrabiania wyświetlanej nazwy;
- **Ocena końcowa:** 🟥 Phishing

| Gdzie?            | Obserwacje                                                                                                      | Wniosek |
|---                |---                                                                                                               |---|
| Nadawca (From)    | `"UPS"` <…@chipcrack[.]es>                                                                                       | **Metoda na podrabianie wyświetlanej nazwy** |
| Return-Path/DKIM  | `Return-Path: …@chipcrack[.]es`, `DKIM d=chipcrack[.]es (rsa-sha1)`                                              | Podpis atakującego, nie marki; DKIM nie uwiarygadnia UPS. |
| Łańcuch Received  | `from aaa.altnewlywed[.]shop `                                                                                   | Wysyłka z losowej domeny, nie infrastruktury UPS. |
| Domena linku (CTA)| `hxxp://5[.]231[.]202[.]248/...`                                                                                 | **Surowy IP** i **brand–domain mismatch** → |
| Treść             | „**nie ma już czasu**” (alarmizm)                                                                                | **Socjotechnika** – presja czasu. |
| Styl/HTML         | Tabelkowy szablon, klasy generatora, zewnętrzne proxy dla logo                                                   | Kopia layoutu, niska jakość, brak spójności z marką. |
| Grafiki           | Obraz z `i.imgur[.]com`                                                                                          | Assety hostowane poza marką - nietypowe dla UPS |
| Stopka            | „Unsub” IP `5[.]231[.]202[.]248`; oraz piksel `chipcrack[.]net/track/...`                                        | Link **nie** prowadzi do UPS; tracking kampanii. |

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

| Pole | Wartość | Notatka |
|---|---|---|
| `From` |  | np. Nie pasuje do marki |
| `Reply-To` | … | np. Inna domena niż `From` |
| `Return-Path` | … | np. Często domena faktycznej wysyłki |
| `Received` (ostatni hop) |  | np. Geolokacja/ASN odbiega od oczekiwanej |
| **SPF** |  |  |
| **DKIM** |  | jw. |
| **DMARC** |  | jw. |


### Tabela IOC

| Type        | Value                                           | Context                                   | First Seen  | Confidence |
|-------------|--------------------------------------------------|--------------------------------------------|-------------|-----------|
| Domain      |                               |         |             | High      |
| URL         |  |   |             | High      |
| Subject     |                       |                              |             | Medium    |
| Phrase      |                 |            |             | Medium    |
| IP          |                                                 |         |             | Low       |
| Email       |                                                 |                     |             | Low       |

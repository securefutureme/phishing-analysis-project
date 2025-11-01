# Email 02 / Credential phishing

**Mail użyty z malware-traffic-analysis.net ------- Użycie tylko dla celów treningowych / edukacyjnych**

Biorąc się do analizy maila pobranego z świetnej strony ze zbiorem malware i maili phishingowych (co jest niesamowitym wsparciem dla każdego, kto chce trenować swoje umiejętności analityczne potrzebne do SOC i nie tylko), widzimy od razu, że mail został skonstruowany tak, żeby przyciągnąć naszą uwagę. Jakbyśmy zamienili się w zwykłego użytkownika, który otwiera skrzynkę mailową i dostaje takiego maila (zakładając, że korzystamy ze strony malware-traffic-analysis.net), dostajemy informację, że mail przyszedł z Supportu znanej nam strony.

Pierwsza czerwona flaga jaka jest tutaj, to rozjechanie się tytułu nadawcy **„malware-traffic-analysis.net Support”,** w stosunku do adresu mailowego nadawcy **sues@nnwifi[.]com** i to właśnie rozjechanie nazwy marki z realnym adresem pozwala nam sądzić, że jest to phishing. Z punktu widzenia użytkownika „Support” brzmi wiarygodnie, ale klient pocztowy pokazuje prawdę: nadawcą jest **sues@nnwifi[.]com**, czyli zupełnie inna domena niż ta użyta w tytule nadawcy. 

Dodamy do tego jeszcze **„Warning: Final notice”** - gdzie od razu widać, że to **typowy chwyt socjotechniczny na wywarcie presji czasu**. Widzimy tu dwie największe czerwone flagi, na które zwracamy uwagę przy analizie phishingu.

<p align="center">
  <img src="/screenshots/mail2/header1.png" alt="Podgląd nagłówka" width="60%">
</p>
<p align="center">
  <em>Rys. 1 — Nagłówki</em>
</p>

Zagłębiając się dalej w maila, w treści wiadomości pojawia się prośba o „**potwierdzenie własności adresu**” z linkiem prowadzącym poza domenę odbiorcy. Po najechaniu kursorem widać **dwie docelowe lokalizacje**:

- `hxxps://servervirto[.]com[.]co/ed/trn/update?email=…`
  
- (przez wrapper Google) → `hxxp://em[.]osanewsletter[.]com/admin/includes/00/update?email=[[Email]]`

To **brand–domain mismatch** w czystej postaci. Dodatkowo, link przez Google (`www.google.com/url?q=…`) służy do maskowania faktycznego celu.

<p align="center">
  <img src="/screenshots/mail2/body1.png" alt="Podgląd nagłówka" width="60%">
  </p>
  <p align="center">
    <em>Rys. 2 — Treść wiadomości</em>
</p>

W nagłówkach wiadmości zdobywamy coraz więcej dowodów. Ostatni hop to mail[.]nnwifi[.]com (173[.]46[.]174[.]49) — to z tego serwera wiadomość trafiła do adresata. Niżej widzimy kilka przeskoków po localhost (127.0.0.1) przez amavisd-new (jest to swego rodzaju "pośrednik” między serwerem pocztowym (MTA, np. Postfix) a skanerami treści, który działa na tym samym hoście); to nie są osobne serwery w Internecie, tylko wewnętrzne przekazania w obrębie mail.nnwifi.com. Najważniejszy jest jednak najniższy wpis:

- **Received: from nnwifi[.]com (94[.]100[.]31[.]27) by mail[.]nnwifi[.]com with ESMTP**

Żeby to ubrać w słowa najprościej - nadanie nastąpiło z hosta nnwifi[.]com (IP 94[.]100[.]31[.]27) z użyciem ESMTP (czyli uwierzytelnionego zgłoszenia przez klienta). **Czyli ktoś zalogował się do serwera mail[.]nnwifi[.]com i wysłał wiadomość jako „Support”, po czym lokalny MTA przepuścił to przez swoje filtry i wysłał dalej.** To wygląda na zwykły serwer/hosting nadawcy kampanii, **nie** infrastrukturę
malware-traffic-analysis[.]net.

Trzy różne domeny w jednej wiadomości pozwalają nam zatwierdzić wniosek, że jest to phishing. Nadawca (nnwifi.com), marka w nazwie (malware-traffic-analysis[.]net), oraz cel linku (servervirto[.]com[.]co / em[.]osanewsletter[.]com przez wrapper Google). Legalne powiadomienia rzadko mieszają tyle przestrzeni nazw.

---

## Podsumowanie

- **Motyw:** podszycie się pod dział wsparcia skrzynki i przekierowanie na zewnętrzne strony kampanii w celu wyłudzenia poświadczeń.
- **Typ ataku:** masowy phishing z **podszyciem pod markę** oraz **spoofingiem nazwy wyświetlanej** (atak linkowy).
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

# Projekt - Analiza maila phishingowego 

| #  | Nazwa analizy | PL                                     | ENG                                                             
|----|--------------------------|----------------------------------------|---------------------------------------------|
| 01 | UPS   | [Mail 1](documentation/email-01-PL.md) | [Mail 1](documentation/email-01-ENG.md) |
| 02 |        | [Mail 2](documentation/email-02-PL.md) | [Mail 1](documentation/email-02-ENG.md) |
| 03 |          | [Mail 3](documentation/email-03-PL.md) | [Mail 1](documentation/email-03-ENG.md) |
| 04 |           | [Mail 4](documentation/email-04-PL.md) | [Mail 1](documentation/email-04-ENG.md) |
| 05 |          | [Mail 5](documentation/email-05-PL.md) | [Mail 1](documentation/email-05-ENG.md) |

## Wstęp

W tym repo prezentuję krótkie, praktyczne analizy **realnych** (oraz fikcyjnych, zaczęrpniętych z różnych źródeł) maili phishingowych. Umiejętność rozpoznawania czerwonych flag i weryfikacji autentyczności jest kluczowa, ponieważ:

- Użytkownikom pozwala nie kliknąć i zatrzymać incydent u źródła. Wbrew pozorom to właśnie tutaj powstaje najwięcej incydentów naruszającym bezpieczeństwo.
- Helpdesk/SOC ułatwia szybką triage i eskalację (blokady domen/IP, IOC do SIEM), co skraca czas reakcji.
- Admnistratorom/bezpieczeństwu daje podstawę do twardych kontroli (DMARC, filtrowanie, makra, zgłaszanie jednym kliknięciem).
- Kadrze kierowniczej zapewnia jasne rekomendacje ograniczające ryzyko i koszty (fraud, przestoje, kary).

**Adresuję moje repo do:**
- użytkowników – jak rozpoznać phishing i czego nie robić;
- SOC/IT – jako przykładowy sposób opisywania analizy phishingu;
- organizacji – w celach szkoleniowych;

## Co to jest phishing?
Phishing jest to metoda oszustwa opierająca się na **“podszywaniu”** się pod inną osobę albo instytucję, próbując w ten sposób **wyłudzić poufne dane, zainfekować komputer czy inne nieprzyjazne działania.**

### Przykłady phishingu:

**Spear phishing** jest celowany mail do konkretnej osoby/zespołu, z detalami z OSINT („Cześć Kasiu, z HR…”) i linkiem/załącznikiem do kradzieży haseł lub malware.

**Vishing** inaczej voice phishing - oszustwo telefoniczne, w którym przestępcy podszywają się pod zaufane instytucje (np. banki, policję) lub osoby, aby wyłudzić poufne dane osobowe.

**Smishing** inaczej SMS phishing - jest to SMS z linkiem do fałszywej wiadomości, zawierającą np. fałszywe linki, bramki płatności/śledzenia paczki lub „dopłaty 3,99 zł”.

**Whaling / CEO Fraud** - atak na kadrę (CEO/CFO); zawiera socjotechnikę "poczucia wyższego szczebla", mail „od prezesa” z prośbą o pilny przelew lub poufne dane.

**BEC - Business Email Compromise** - zwykle jest to przejęta prawdziwa skrzynka firmy/partnera; zamieniane są numery kont na fakturach, wiadomość z „aktualizacja danych płatności” itp. 

**SEO poisoning / Search Engine Phishing** złośliwe strony wypchnięte wysoko w Google (często reklamy); użytkownik klika „pobierz Teams/Bank” i trafia na podróbkę.

**Clone phishing** - imitowaniu legalnych wiadomości e-mail od zaufanych firm w celu nakłonienia ofiar do ujawnienia poufnych informacji.

**QR phishing (QRishing)** – przestępca tworzy kod QR, który jest wysyłany w mailu/ulotce i zwykle prowadzi do fałszywej strony logowania albo też do strony atakującego.

**Consent/OAuth phishing** – zamiast hasła prosi o „Zgódź się na dostęp” dla rzekomej aplikacji; w rzeczywistości oddajesz tokeny do konta.

**MFA fatigue – jest to technika „bombardowania”** push'ami MFA do ofiary, aż zaakceptuje "przypadkowo".

**Tech support / angler phishing** – jest fałszywy czat/ogłoszenie „pomocy technicznej” (często na social media), namawia do instalacji narzędzi zdalnych.

**Pharming/Wi-Fi captive hijack** – przekierowaniu użytkownika na fałszywą stronę (np. poprzez manipulację systemem DNS lub plikiem hosts), która wygląda identycznie jak legalna strona, zmuszając ofiarę do samodzielnego wpisania danych.

**Watering hole** – zainfekowanie strony często odwiedzanej przez cel (np. branżowy portal), by złowić loginy/zaszczepić malware.


## Co znajdziesz:
- opisy case-by-case (`documentation/`),
- treści i nagłówki maila (`analysis/`),  
- zrzuty ekranu (`screenshots/`),  

**Workflow:**
VM → eksport maili phishingowych -> eksport treści/nagłówków →  analiza wedle schematu -> toole analizujące adresy IP i linki → **Tabela IOC** 


### INFO
**Niektóre dane, jak mój adres mailowy i inne zostały usunięte, z powodów prywatnych.**

**Ten projekt jest ćwiczeniem obrazującym moje umiejętności analizy maila phishingowego po odbyciu kursu Szkoła Security.**

# Analiza maila phishingowego / Phishing mail analysis

## Indeks analiz

| #  | Nazwa analizy / Analysis name            | PL                                     | ENG                                         | Body | Headers | Screens |
|----|--------------------------|----------------------------------------|---------------------------------------------|------|---------|---------|
| 01 | UPS threat in private mail    | [Case 01](documentation/case-01-netflix.md) | [Case 01 ENG](documentation/case-01-netflix-ENG.md) | [txt](analysis/body1.txt) | [txt](analysis/headers1.txt) | [dir](screenshots/) |
| 02 | M365 re-auth             | [Case 02](documentation/case-02-m365-reauth.md) | [ENG](documentation/case-02-m365-reauth-ENG.md) | [txt](analysis/body2.txt) | [txt](analysis/headers2.txt) | [dir](screenshots/) |
| 03 | GoDaddy billing          | [Case 03](documentation/case-03-godaddy-billing.md) | [ENG](documentation/case-03-godaddy-billing-ENG.md) | — | — | — |
| 04 | Parcel fee               | [Case 04](documentation/case-04-parcel-fee.md) | [ENG](documentation/case-04-parcel-fee-ENG.md) | — | — | — |
| 05 | Webmail quota            | [Case 05](documentation/case-05-webmail-quota.md) | [ENG](documentation/case-05-webmail-quota-ENG.md) | — | — | — |

![Widok maila](screenshots/01_mail_view.png)

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

## Czym jest mail phishingowy (w skrócie)
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

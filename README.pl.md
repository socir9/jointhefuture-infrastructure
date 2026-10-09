# JoinTheFuture — Własny serwer i automatyzacja poczty

**DevOps / Backend / Administracja Linux** · [Działająca strona: jointhefuture.pl](https://jointhefuture.pl/)

[English version](README.md)

> **Opis projektu do portfolio.** To repozytorium przedstawia moją pracę przy infrastrukturze i backendzie strony JoinTheFuture. **Nie jest** kopią kodu źródłowego strony ani produkcyjnej konfiguracji serwera.

## O projekcie

Hostuję stronę JoinTheFuture na **własnym serwerze Linux**. Zajmuję się jej infrastrukturą i utrzymaniem, usługami opartymi na **Dockerze i Caddy**, automatyzacją wdrażania oraz backendem formularza kontaktowego.

Formularz korzysta z **backendu napisanego w Pythonie** na własnej infrastrukturze. Wiadomości wysyłane są przez **SMTP Hostinger** — bez konieczności korzystania z zewnętrznej usługi obsługującej formularze.

| Obszar | Moja praca i technologie |
| --- | --- |
| Hosting | Własny serwer Linux, utrzymanie usług i strony |
| Kontenery i routing | Docker, Caddy, reverse proxy, HTTPS i certyfikaty TLS |
| Backend | Obsługa formularza kontaktowego w Pythonie |
| Automatyzacja e-mail | Integracja z SMTP Hostinger i przechowywanie danych dostępowych po stronie serwera |
| Wdrażanie | GitHub Actions, budowanie, testy kontrolne, wdrożenia przez SSH |
| Niezawodność | Health checki, zabezpieczenia formularza, kopie przed wdrożeniem i procedury przywracania |

## Architektura — uproszczony schemat

Diagram przedstawia **logiczne elementy systemu**, a nie dokładną topologię wewnętrznej sieci. Pomija celowo szczegóły konfiguracji i ewentualne pośrednie reverse proxy.

~~~mermaid
flowchart TD
    A["Użytkownik / przeglądarka"]
    B["Strona JoinTheFuture<br/>Własny serwer Linux"]
    C["Caddy<br/>HTTPS / reverse proxy"]
    D["Formularz kontaktowy"]
    E["Backend Python"]
    F["SMTP Hostinger"]
    G["Wiadomość / potwierdzenie e-mail"]

    A -->|"HTTPS"| C
    C --> B
    B --> D
    D -->|"Żądanie do backendu"| E
    E -->|"SMTP / TLS"| F
    F --> G
~~~

**Strona** działa na własnym serwerze. **Caddy** obsługuje publiczne połączenia HTTPS, a **backend formularza** przetwarza zgłoszenia i przekazuje wiadomości do Hostinger SMTP. Infrastruktura korzysta również z Dockera. Dokładny układ wewnętrznych usług może się zmieniać.

## Zakres mojej pracy

### Hosting i administracja serwerem

- Utrzymanie środowiska serwerowego rzeczywistej strony internetowej.
- Obsługa usług Dockera oraz routingu HTTPS w Caddy.
- Oddzielenie publicznej strony od prywatnej konfiguracji usług.

### Backend Python i automatyzacja e-mail

- Obsługa formularza przez backend Pythona działający na własnej infrastrukturze.
- Wysyłanie zgłoszeń oraz potwierdzeń przez SMTP Hostinger.
- Przechowywanie danych SMTP na serwerze, a nie w kodzie frontendu.
- Walidacja żądań i zabezpieczenia, m.in. limity rozmiaru, ochrona przed spamem i ograniczanie częstotliwości żądań.

### Automatyzacja wdrażania

Repozytorium strony używa **GitHub Actions** do budowania, weryfikowania poprawności adresów URL i wdrażania plików na własny serwer. Workflow przekazuje również pliki backendu formularza i może uruchamiać przygotowany po stronie serwera mechanizm wdrożeniowy.

~~~mermaid
flowchart LR
    A["Zmiany na main"]
    B["GitHub Actions"]
    C["Build i kontrola"]
    D["Wdrożenie na serwer"]
    E["Działająca strona"]

    A --> B --> C --> D --> E
~~~

Kod oryginalnej strony i dane dostępowe do wdrażania pozostają prywatne.

## Technologie

**Linux** · **Docker** · **Caddy** · **Python** · **SMTP (Hostinger)** · **GitHub Actions** · **SSH** · **HTTPS/TLS** · **JavaScript**

## Dlaczego ten projekt jest ważny?

Pokazuje praktyczne doświadczenie z **utrzymywaniem prawdziwej infrastruktury na własnym serwerze**, integracjami backendowymi, automatyzacją wdrożeń i ochroną danych dostępowych — nie jest to tylko aplikacja uruchomiona lokalnie do nauki.

## Potwierdzenie projektu i poufność

- **Działająca strona:** https://jointhefuture.pl/
- **Mój GitHub:** https://github.com/socir9
- Repozytorium źródłowe strony jest prywatne. Ten opis nie daje do niego dostępu.
- Nie publikuję kodu aplikacji, prywatnych adresów serwerowych, plików środowiskowych, danych logowania, haseł SMTP, wiadomości klientów ani wewnętrznych instrukcji operacyjnych.
- Diagramy ilustrują sposób działania systemu, ale **nie są kompletną konfiguracją do odtworzenia produkcyjnego serwera**.

---

**Autor portfolio:** [@socir9](https://github.com/socir9)  
**Obszary:** Self-hosting, praktyki DevOps, backend Python i automatyzacja poczty.

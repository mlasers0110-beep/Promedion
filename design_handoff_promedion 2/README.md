# Handoff: Promedion — Strona fuzji technologicznej (landing page)

## Overview
Jednostronicowy, ciemny ("deep-ocean") landing page przedstawiający strategiczną fuzję
Kliniki Promedion (chirurgia plastyczna) z parkiem technologicznym napędzanym AI.
Strona jest pitch‑deckiem dla decydentów kliniki: prezentuje infrastrukturę, listę
urządzeń ("Hi‑Tech"), model współpracy (joint‑venture), inteligencję rynkową i kontakt.
Centralnym elementem wizualnym jest animowana, falująca sieć kolagenowa renderowana na
`<canvas>` w sekcji hero.

## About the Design Files
Pliki w tej paczce to **referencje projektowe stworzone w HTML** — prototyp pokazujący
docelowy wygląd i zachowanie, **nie** kod produkcyjny do bezpośredniego skopiowania.
Zadaniem jest **odtworzenie tych projektów w docelowym środowisku** (np. Next.js + React,
co jest naturalne, bo źródłem był projekt Next.js) z użyciem przyjętych w nim wzorców i
bibliotek. Jeśli repo nie ma jeszcze środowiska, należy wybrać najwłaściwszy framework
(rekomendacja: **Next.js / React + TypeScript**) i zaimplementować projekt tam.

Plik `Promedion.dc.html` jest napisany w wewnętrznym formacie "Design Component" (znaczniki
`<x-dc>`, `<helmet>`, `{{ ... }}`, `data-reveal`). Traktuj go jako **specyfikację wizualną
i behawioralną**, nie jako moduł do importu. `Promedion-standalone.html` to samodzielna,
offline'owa wersja do podglądu w przeglądarce.

## Fidelity
**High‑fidelity (hifi).** Finalne kolory, typografia, odstępy, animacje i pełne copy (PL).
Odtwórz UI 1:1, używając bibliotek i wzorców istniejących w docelowym repo.

## Design Tokens

### Kolory
- Tło główne / najciemniejsze: `#03060d`
- Tło sekcji ciemne: `#04101f`
- Tło najgłębsze (gradient stops): `#020a16`
- Gradient akcentowy (hero/arsenal/kontakt): `radial-gradient(120% 90% at 50% 0%, #0a2540 0%, #04101f 38%, #020a16 70%, #03060d 100%)`
- Tekst jasny (nagłówki): `#eaf1f8`
- Tekst body (domyślny): `#c9d6e4`
- Tekst body przygaszony: `rgba(201,214,228,0.6–0.8)`
- Akcent "filament" (cyjan): `#bfe9ff`
- Akcent przygaszony / obramowania / poświata: `rgba(191,233,255,0.08–0.6)`
- Szkło (glass card) tło: `linear-gradient(160deg, rgba(14,51,84,0.35), rgba(4,16,31,0.25))`
- Selekcja tekstu: tło `rgba(191,233,255,0.18)`, kolor `#eaf1f8`

### Typografia
- Nagłówki (serif): **Cormorant Garamond**, wagi 300/400/500/600 + italic 400/500.
  H1/H2 zwykle `font-weight:300`, akcenty kursywą w kolorze `#bfe9ff`.
- Body / UI (sans): **DM Sans**, wagi 300/400/500.
- Import: Google Fonts — `family=Cormorant+Garamond:ital,wght@0,300;0,400;0,500;0,600;1,400;1,500&family=DM+Sans:wght@300;400;500`
- Skale nagłówków: H1 hero `clamp(44px,7vw,82px)`, H2 sekcji `clamp(32px,4.6vw,50px)`,
  H1 podstrony manifestu `clamp(34px,5.5vw,60px)`.
- Eyebrow (nadtytuł): 12px, `text-transform:uppercase`, `letter-spacing:0.4em`, `rgba(191,233,255,0.6)`.
- Body sekcji: 18px, `font-weight:300`, `line-height:1.7`.

### Odstępy / układ
- Szerokości kontenerów: `max-width:1152px` (szerokie sekcje), `1024px` (manifest/synergia),
  `896px` (kontakt), `820px` (artykuł manifestu).
- Padding pionowy sekcji: `128px 0`. Padding poziomy: `0 24px`.
- Border radius: karty/panele `16px`, przyciski/kapsułki/pill `999px`.
- Cień kart: `0 18px 50px rgba(2,10,22,0.55)`.
- Glass: `backdrop-filter: blur(10–14px)` (+ `-webkit-`).

### Animacja "reveal" (wejście przy scrollu)
- Stan początkowy: `opacity:0; transform:translateY(26px)`.
- Przejście: `opacity 1.1s cubic-bezier(.22,1,.36,1), transform 1.1s cubic-bezier(.22,1,.36,1)`.
- Wyzwalane przez IntersectionObserver (patrz `componentDidMount` w `Promedion.dc.html`).
  Opóźnienia per element przez atrybut `data-reveal-delay` (sekundy).

## Screens / Views

### 1. Header / nav (fixed)
- Pozycja: `position:fixed`, top, `z-index:50`, max‑width 1152px, padding 24px.
- Logo tekstowe: "PRO" (`#eaf1f8`) + "MEDION" (`#bfe9ff`), Cormorant Garamond 21px.
- Nawigacja (ukrywana <820px): linki kotwiczące — **Manifest** (#manifest), **Hi‑Tech**
  (#arsenal), **Synergia** (#synergia), **Rynek** (#rynek). Linki 11px uppercase,
  `letter-spacing:0.25em`, hover → `#eaf1f8`.

### 2. Hero (#hero)
- Pełnoekranowa sekcja z `<canvas>` w tle (animowana sieć kolagenowa, patrz "Canvas").
- Eyebrow: "Promedion · Medycyna precyzyjna".
- H1: "Rewolucja AI to za mało." / "Czas na *technologiczną hegemonię.*" (druga część
  kursywą, `#bfe9ff`), `text-shadow:0 0 28px rgba(191,233,255,0.22)`.
- Podtytuł: "Chirurgia perfekcyjna. Rekonwalescencja do optymalizacji."
- CTA: przycisk "Zobacz architekturę współpracy" (pill, tło `rgba(191,233,255,0.9)`,
  tekst `#020a16`, hover `#eaf1f8`) → kotwica #arsenal; obok link‑ghost → #manifest.
- Wskaźnik scroll z animacją `promScroll`.

### 3. Manifest kliniczny (#manifest)
- Tło `#03060d`. Górny gradient‑fade nakładki.
- Lewa kolumna: eyebrow "Manifest kliniczny", H2 "Infrastruktura, która deklasuje
  konkurencję.", przycisk **"Manifest"** (pill, obramowanie `rgba(191,233,255,0.3)`,
  szkło) → otwiera pełnoekranową podstronę manifestu (patrz #10).
- Prawa kolumna: `figure` ze zdjęciem `assets/jan-bujok.jpg` (200px szer., 270px wys.,
  `object-fit:cover`, radius 16px, obramowanie + cień), podpis "Jan Bujok" /
  "Architekt fuzji technologicznej".
- Dwa akapity body + rząd 3 statystyk w siatce (X‑Rite / 0,01 mm / 9), karty `1px`
  separowane, radius 16px.

### 4. Hi‑Tech / Arsenał (#arsenal)
- Gradient akcentowy w tle. Eyebrow "Hi‑Tech", H2 "Pełny park technologiczny. Jedna
  macierz decyzyjna."
- Siatka 6 kart‑urządzeń (glass, radius 16px, hover: `translateY(-6px)` + jaśniejsze
  obramowanie + podświetlenie `[data-arsenal-underline]`). Każda karta: etykieta
  (uppercase, `rgba(191,233,255,0.5)`), tytuł serif 24px, opis 14px, dolna linia‑gradient.
  M.in. "Laser Pikosekundowy <350ps", "Mapowanie X‑Rite" (etykieta "myskinecode.ai"), itd.
- Pod kartami: rząd **kapsułek/pill** (`data-arsenal-pill`, flex‑wrap, gap 14px) z 11
  dodatkowymi urządzeniami: Laser tulowy (1927nm), Laser Er:Yag‑szkło, Plazma fuzyjna,
  Fotobiomodulacja LED, HIFFEM + IR, Platforma Laserowa 430‑750nm, Laser Nd:Yag
  (0,1ms–100ml), Laser Aleksandrytowy 755nm, EMS+EMT+RF, Laser diodowy – FVLT/LHP/FiLaC,
  Laser Diodowy 755+810+980+1064nm.

### 5. Synergia (#synergia)
- Tło `#03060d`. H2 "Nowy wymiar zyskowności bez obciążania bloków operacyjnych."
- Wprowadzenie: "Współpraca ma charakter strategicznego joint‑venture."
- Trzy filary (01/02/03): "Gwarancja Zdrowej Blizny & Fast Recovery", "Nowy strumień
  pacjentów", "Zero nakładów inwestycyjnych (CapEx) dla Kliniki" — każdy z opisem.

### 6. Rynek / Inteligencja rynkowa (#rynek)
- Tło `#04101f`. Eyebrow "Inteligencja rynkowa i strategia akwizycji".
- H2 "Znamy architekturę konkurencji. *Przejmujemy ich pacjentów.*"
- Wprowadzenie + 3 karty konkurencji (Skingen Clinic — Izabelin; OT.CO — Bielany;
  Miracki · Warsaw Aesthetic — południe Warszawy), styl jak karty arsenału.
- Panel "Niezależność operacyjna — Marketing & Ads".
- Finał: duża serifowa kursywa z podświetleniem "europejskiej top‑ligi medycyny estetycznej".

### 7. Kontakt (#kontakt)
- Gradient akcentowy. Wyśrodkowane. H2 "Technologia jest gotowa. Procedury są opisane."
- Treść z podświetleniem "technologicznym liderem medycyny estetycznej w Polsce" +
  "Spotkajmy się, by omówić liczby i protokoły medyczne."
- Dwa przyciski: `mailto:drbujok@gmail.com` ("drbujok@gmail.com", pill solid) i
  `tel:+48535533059` ("535 533 059", pill ghost).

### 8. Footer
- Stopka: "© 2026 bmclinics.ai — made by Jan Bujok".

### 9. Cookie banner + Privacy overlay
- Banner cookies (stan `cookieChoice` w localStorage), overlay polityki prywatności
  (`showPrivacy`, `activeDoc`).

### 10. Podstrona Manifestu (overlay /manifest)
- Pełnoekranowy overlay (`showManifest`, `position:fixed; inset:0; z-index:400`),
  gradient‑tło, sticky‑header z logo i przyciskiem zamknięcia.
- Eyebrow "Manifest kliniczny · pełna wersja", H1 "Wprowadzenie i parametryzacja
  metodologiczna procesu akwizycji obrazu", dwa pełne akapity tekstu klinicznego
  (kalibracja X‑Rite, BRDF, profilometria optyczna, osie patomorfologiczne) z
  przypisami `<sup>`. Przycisk "← Powrót do strony".
- W docelowym repo zaimplementuj to jako **realną podstronę `/manifest`** (route), nie
  jako modal — taka była intencja zamawiającego.

## Interactions & Behavior
- **Reveal on scroll**: IntersectionObserver dodaje stan widoczny do `[data-reveal]`,
  z opóźnieniem `data-reveal-delay`.
- **Nawigacja kotwicowa**: smooth scroll (`scroll-behavior:smooth`).
- **Manifest**: przycisk otwiera podstronę/overlay; w produkcji → route `/manifest`.
- **Hover**: karty unoszą się i rozjaśniają obramowanie; pill/CTA zmieniają tło/obramowanie.
- **Cookies/Privacy**: zapis wyboru, pokazywanie/ukrywanie overlay.
- **Responsywność**: nav chowa się <820px; siatki używają `auto-fit/minmax`.

## Canvas — animowana sieć kolagenowa (hero)
- `<canvas>` rysowany w `requestAnimationFrame`. Węzły w siatce falują (sumy sinusów),
  z perspektywą (`persp = 1 + z*0.014`), oddechem (breath), opcjonalną turbulencją,
  oraz powolnym dryfem/rotacją całej siatki ("swirl").
- Sterowanie przez propsy (Tweaks), czytane na żywo każdej klatki, z akumulatorem czasu
  (zmiana prędkości nie powoduje skoku):
  - `networkSpeed` (0.2–3.5, domyślnie ~2.9) — tempo.
  - `networkAmplitude` (0.5–3, domyślnie ~2.6) — siła ruchu węzłów.
  - `networkCharacter` ("calm" | "living" | "turbulent", domyślnie "turbulent") — profil
    [turbulencja, breath‑freq, breath‑var]: calm `[0,0.30,0.12]`, living `[0.5,0.45,0.22]`,
    turbulent `[1.15,0.72,0.36]`.
  - `networkSwirl` (0–3, domyślnie ~2.5) — dryf i rotacja całej siatki.
- W produkcji: wyodrębnij jako komponent `<CollagenNetwork />` z tymi propsami; pełna
  logika rysowania jest w `Promedion.dc.html` (klasa `Component`, metoda `componentDidMount`).

## State Management
- `cookieChoice` (undefined | null | boolean) — wybór cookies (persist w localStorage).
- `showPrivacy` (boolean), `activeDoc` ('privacy' | ...) — overlay dokumentów prawnych.
- `showManifest` (boolean) — widoczność manifestu (→ route w produkcji).
- Parametry canvasu (`networkSpeed/Amplitude/Character/Swirl`) — propsy/konfiguracja.

## Assets
- `assets/jan-bujok.jpg` — portret (źródło: upload użytkownika `IMG_8121 6.jpg`).
  Wyświetlany 200×270, `object-position:50% 18%`, `filter:saturate(0.92) contrast(1.02)`.
- Fonty: Google Fonts (Cormorant Garamond, DM Sans) — w produkcji użyj
  `next/font` lub odpowiednika.
- Brak innych obrazów; sieć kolagenowa jest rysowana proceduralnie na canvas.

## Files
- `Promedion.dc.html` — źródłowy "Design Component" (specyfikacja wizualna + logika canvas).
- `Promedion-standalone.html` — samodzielna wersja offline do podglądu w przeglądarce.
- `assets/jan-bujok.jpg` — zdjęcie używane w sekcji Manifest.

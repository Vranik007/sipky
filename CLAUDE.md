# Šipky 501 – počítadlo

Jednoduchá webová aplikace na počítání šipek, celá v jednom souboru `sipky.html`
(styly i skripty uvnitř, žádné knihovny, žádný server – otevírá se přímo v prohlížeči).

GitHub: https://github.com/Vranik007/sipky (veřejný repozitář, větev `main`)

**Živá stránka:** https://vranik007.github.io/sipky/ (GitHub Pages z větve `main`, kořen).
Každý push na `main` stránku do ~1 minuty sám aktualizuje. `index.html` jen
přesměrovává na `sipky.html`. Repozitář je veřejný, protože Pages na bezplatném
účtu jinak nejdou – nikdy do něj nedávat hesla ani osobní údaje.

**Instalace na telefon:** `manifest.webmanifest` + ikony (`icon-192.png`, `icon-512.png`,
`apple-touch-icon.png` – terč v barvách aplikace) umožní „Přidat na plochu“ a otevírání
přes celou obrazovku bez adresního řádku. Ikony byly vygenerovány krátkým Python skriptem
bez knihoven (PIL v počítači není) – při změně ikony je potřeba je vygenerovat znovu.

## Pravidla hry v aplikaci
- Hra 501, **double out** (zakončení musí být na dvojku nebo bull).
- 2–4 hráči, zadává se součet bodů za kolo (3 šipky) přes klávesnici na obrazovce.
- Neplatná skóre (nad 180 nebo nehoditelná třemi šipkami) se odmítnou.
- Přehoz (pod 0 nebo zbyde 1) = skóre zůstává, hraje další hráč.
- Při přesném dohození na 0 se aplikace zeptá, jestli to byla dvojka.
- Každý další leg začíná další hráč v pořadí.

## Pravidla pro úpravy
- **Herní obrazovka se musí vejít na displej bez posouvání** – na počítači i na mobilu
  (úzký displej do 700 px má vlastní, úspornější rozložení).
- Kruhový ukazatel zbývajícího skóre je **v panelu hráče nahoře, kolem čísla**
  (plný při 501, ubírá se k 0; zelený = hráč na tahu, žlutý = zbývá 170 a méně).
  Kruhy u klávesnice uživatel nechtěl.
- Panely hráčů se staví jednou na začátku hry (`buildPanels`) a pak se jen
  aktualizují (`render`) – kvůli plynulé animaci kruhu. Nepřestavovat je při každém hodu.
- Texty v aplikaci jsou česky.

## Testování
Prohlížeč přes Claude in Chrome neotevře `file://`, proto spustit dočasný server:
`python -m http.server 8765 --bind 127.0.0.1` a otevřít `http://127.0.0.1:8765/sipky.html`.
Mobil lze simulovat vložením stránky do `<iframe>` širokého 400 px.
Po testu server vypnout.

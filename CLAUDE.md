# Cinnery Counter – fejlesztői jegyzet

Napi/havi/éves forgalmi dashboard a Cinnery pékségnek, egyetlen statikus `index.html` (nincs build, nincs keretrendszer). Felhasználói leírás: README.md.

## Indítás és ellenőrzés
- `python3 -m http.server <port>` a repó gyökeréből (nincs állandó launch config; ideiglenes bejegyzés a `~/Claude_code/.claude/launch.json`-ba, ha kell).
- Ellenőrzés: mindhárom nézet (Day / Month / Year) mindhárom nyelven, világos+sötét téma, konzolhiba nélkül.
- Színek ellenőrzése: a dataviz skill palettavalidátorával (Node szkript).

## Felépítés
- `index.html` – minden: stílus, `I18N` objektum (az angol szöveg a saját kulcsa, csak a fordítások vannak felsorolva), `genDay()` demóadat-generátor, `LIVE_DAYS`, renderelés.
- `robots.txt` (Disallow: /) + `noindex, nofollow` meta. `roll.svg` – ikon.

## Telepítés
- GitHub Pages a `main` gyökeréből (build_type legacy – a repó „workflow” módban jött létre, át kellett állítani és kézzel indítani egy buildet).
- Push után ellenőrzés: a lokális és az élő fájl `shasum`-ja egyezzen (a Pages 1–2 perc).
- Védett másolat a sadrobot infrán is fut (passkey mögött) – lásd /deploy-sadrobot skill (oldal: `cinnery-dashboard`).

## Döntések
1. Két csatorna van: bolti POS (Lightspeed) és előrendelés/átvétel (Order Anywhere). Házhozszállítás sehol nincs a Cinnery-projektben.
2. Lightspeed még nincs bekötve: determinisztikus demó (seedelt PRNG, groningeni diákváros-szezonalitás, nyitás 2025-09-02, mai napnál későbbi nap nincs), a lap „Demo data” jelzést mutat.
3. Valódi adat a `LIVE_DAYS`-be: kulcs = ISO dátum, érték = a `genDay()`-jel azonos alakú objektum; egy ott szereplő nap felülírja a demót és eltünteti a bannert.
4. Nyelv: EN (alap) / NL / HU fejléc-váltóval, localStorage-ban megjegyezve; a hét/hónap nevek, dátumsorrend, szám- és pénzformátum a nyelvet követi.
5. Betűk: Fredoka + IBM Plex Sans/Mono (Google Fonts – itt szándékosan nem él a weboldal „nulla harmadik fél” szabálya). Csatornaszínek: lila #4a3aa7 (POS), rózsaszín #e87ba4 (átvétel), mindkét témában validálva.
6. **Hozzáférés:** a nyilvános Pages csak addig elfogadható, amíg demóadat van rajta. Az első valódi szám előtt a repót priváttá kell tenni és a Pages-t kikapcsolni (különben a régi URL tovább szolgálja), az oldal pedig csak jelszó/passkey mögött futhat.

## Nyitott
- Lightspeed bekötése (valódi napok a `LIVE_DAYS`-be).
- A holland szövegeket anyanyelvű még nem lektorálta.

# Notová cvičení

Generátor tištěných pracovních listů pro procvičování čtení not. Na jedno kliknutí
vytvoří nový list — prázdný notový papír, obtahování klíče nebo cvičení na
pojmenovávání a zapisování not.

Inspirováno [staffpaper.org](https://staffpaper.org/).

## Použití

Otevřete `index.html` v prohlížeči (stačí dvojklik na soubor). Není potřeba žádný
server ani instalace.

1. Nahoře vyberte klíč, typ cvičení a rozsah tónů.
2. **Nový pracovní list** vygeneruje novou náhodnou sadu not.
3. **Tisk** otevře tiskový dialog. Ovládací panel se při tisku automaticky skryje,
   list je formátovaný na A4.

## Typy cvičení

| Typ | Co list obsahuje |
|---|---|
| Prázdný notový papír | Jen čisté osnovy s klíčem, bez not |
| Obkreslování klíče | Plný klíč jako vzor, za ním světle šedé kopie k obtažení tužkou |
| Nota → pojmenuj | Nota na osnově a prázdný rámeček na zapsání názvu tónu |
| Písmeno → umísti notu | Název tónu nad prázdnou osnovou, nota se dokresluje |

Klíč lze zvolit houslový, basový, nebo oba dohromady (velká osnova). Rozsah tónů je
volitelný; pokud tón přesahuje osnovu, program automaticky přidá pomocné linky.

## Značení oktáv

Program používá **české značení oktáv** podle hudební nauky, ne vědecké (scientific
pitch) značení:

| Oktáva | Značení |
|---|---|
| dvoučárkovaná | `c2`, `d2`, … |
| jednočárkovaná (střední C) | `c1`, `d1`, … |
| malá | `c`, `d`, … |
| velká | `C`, `D`, … |
| kontra | `C1`, `D1`, … |

Střední C se tedy zobrazuje jako `c1` (nikoli `C4`).

## Struktura projektu

```
index.html            celá aplikace — HTML, CSS a JavaScript v jednom souboru
fonts/
  Bravura.otf         notopisný font Bravura
  Bravura.woff2       tentýž font ve webové variantě
  bravura_metadata.json  SMuFL metadata (rozměry znaků ve mezerách osnovy)
  OFL.txt             licence fontu
```

Aplikace nemá žádné externí závislosti a funguje offline.

## Jak jsou kreslené klíče

Obrysy houslového a basového klíče jsou vektorové cesty vytažené z fontu Bravura a
vložené přímo do `index.html`. Font se tedy nemusí instalovat a list se vykreslí
stejně v každém prohlížeči.

Bravura dodržuje standard [SMuFL](https://w3c.github.io/smufl/), z čehož vyplývá
přesné posazení klíče na osnovu:

- 1 em = 4 mezery osnovy, tedy 1 mezera = 250 jednotek fontu,
- počátek znaku leží na lince, kterou klíč pojmenovává — houslový klíč na lince
  `g` (2. odspodu), basový klíč na lince `f` (2. odshora).

Pozice klíče je proto spočítaná, ne odhadnutá.

## Licence

Font Bravura © 2020 Steinberg Media Technologies GmbH, šířený pod licencí
SIL Open Font License 1.1 — plný text v [fonts/OFL.txt](fonts/OFL.txt).
"Bravura" je Reserved Font Name podle této licence.

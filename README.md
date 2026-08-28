# Školička

Generátor tištěných pracovních listů pro první stupeň. Na jedno kliknutí vytvoří
nový list ve dvou předmětech:

- **Hudební nauka** — prázdný notový papír, obtahování klíče, pojmenovávání
  a zapisování not.
- **Matematika** — sčítání, odčítání a doplňování znamének do 20, znázorněné
  hromádkami ovoce.

Inspirováno [staffpaper.org](https://staffpaper.org/).

## Použití

Otevřete `index.html` v prohlížeči (stačí dvojklik na soubor). Není potřeba žádný
server ani instalace.

1. Nahoře vyberte **předmět** — podle toho se přepnou ostatní volby.
2. Nastavte typ cvičení a jeho parametry.
3. **Nový pracovní list** vygeneruje novou náhodnou sadu úloh.
4. **Tisk** otevře tiskový dialog. Ovládací panel se při tisku automaticky skryje,
   list je formátovaný na A4 a vejde se na jednu stránku bez zmenšování
   v nastavení tisku — viz [Tisk na jednu A4](#tisk-na-jednu-a4).

# Hudební nauka

## Typy cvičení

| Typ | Co list obsahuje |
|---|---|
| Prázdný notový papír | Jen čisté osnovy s klíčem, bez not |
| Obkreslování klíče | Klíč tenkou linkou — první černý jako vzor, další světle šedé k obtažení tužkou |
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

### Středová linka pro obkreslování

Cvičení „Obkreslování klíče“ nepoužívá plný tvar klíče — vybarvovat širokou plochu
tužkou není obtahování. Místo toho se kreslí **středová linka** (osa) klíče: tenká
čára vedená středem tahu.

Ta je odvozená z obrysu Bravury programově: tvar se vykreslí do rastru, ztenčí se
algoritmem Zhang-Suen na linku širokou jeden pixel, ta se převede na křivku,
odstraní se falešné výběžky a výsledek se vyhladí na oblouky. Výsledná cesta je
v `index.html` uložená jako `tracePath` u každého klíče. Tvar tedy odpovídá
skutečnému notopisnému klíči, jen je tenký.

# Matematika

Listy pro prvňáčky. Každá úloha je záměrně jednoduchá — dvě hromádky ovoce
a jeden řádek s příkladem. Ovoce se skládá po pěti kusech do řady, aby se dalo
počítat po pěticích.

## Typy úloh

| Typ | Co list obsahuje |
|---|---|
| Sčítání | Dvě hromádky ovoce se znaménkem `+` a příklad `a + b = ☐` |
| Odčítání | Dvě hromádky ovoce se znaménkem `−` a příklad `a − b = ☐` |
| Sčítání i odčítání | Náhodný mix obou předchozích |
| Doplň znaménko | Dvě hromádky a zápis `☐ ◯ ☐ = výsledek` — dítě doplní obě čísla i znaménko `+` nebo `−` |
| Doplň chybějící číslo | `3 + ☐ = 8` nebo `☐ − 3 = 5` — chybí jeden ze dvou počítaných členů, výsledek je zadaný |
| Rozklad čísla | Hromádka `n` kusů a zápis `n = ☐ + ☐`; správných řešení je víc |
| Porovnávání | Dvě hromádky vedle sebe a zápis `☐ ◯ ☐` — dítě doplní obě čísla i znaménko `<`, `>`, `=` |
| O kolik víc | Dvě hromádky pod sebou a otázka „O kolik víc?" |
| Vše dohromady | Náhodný mix všech typů |

Úlohy se generují tak, aby součet nepřesáhl zvolený obor a aby výsledek odčítání
nikdy nešel do záporných čísel ani na nulu — záporná čísla se probírají mnohem
později. Obě hromádky mají vždy aspoň jeden kus. Zhruba každá čtvrtá úloha na
porovnávání má obě hromádky stejně velké, aby se rovnítko neztratilo mezi samými
nerovnostmi.

Volitelný je **číselný obor** (do 5, do 10, do 20), **znázornění**, **druh ovoce**
(jablka, hrušky, třešně, jahody, pomeranče, nebo náhodně u každé úlohy) a **počet
úloh** na listu.

## Znázornění

| Volba | Co je na kartičce |
|---|---|
| Ovoce i čísla | Hromádky ovoce a pod nimi číselný příklad |
| Jen ovoce | Pouze hromádky ovoce a prázdný zápis `☐ + ☐ = ☐` — dítě doplní i obě počítaná čísla, nikde je nemá předepsaná |
| Jen čísla | Pouze číselný příklad, bez obrázků (výběr ovoce se skryje) |

Na kartičce je vždy jen jeden druh prázdného rámečku — buď se doplňuje do
obrázku, nebo do číselného zápisu, nikdy obojí naráz. U typů, kde se doplňuje
symbol (znaménko, porovnání), je proto ve volbě „Ovoce i čísla" rámeček jen
v zápisu a hromádky nad ním slouží k počítání; ve volbě „Jen ovoce" je rámeček
mezi hromádkami. U typu **Doplň chybějící číslo** je v obrázku na místě
chybějícího členu otazník a rámeček je jen v zápisu; ve volbě „Jen ovoce" žádný
zápis není, takže se rámeček přesune přímo do obrázku.

Hromádky, které nedělí znaménko (porovnávání, „o kolik víc"), jsou orámované
tenkou čárkovanou linkou — zalomená hromádka by jinak splynula s tou vedle.

Rámeček na znaménko je kolečko, rámeček na číslo čtvereček. U porovnávání
a doplňování znaménka tak dítě s obrázkem doplňuje obojí — spočítá hromádky,
zapíše obě čísla do čtverečků a mezi ně do kolečka doplní znaménko. Zadaný
zůstává jen výsledek, ten z hromádek vyčíst nejde. Ve volbě „Jen čísla" jsou
čísla zadaná, jinak by nebylo co porovnávat.

# Tisk na jednu A4

Každý list vyjde na jednu stránku A4 při měřítku 100 %, aniž by bylo potřeba
v tiskovém dialogu cokoli zmenšovat. Platí to pro všechny kombinace typu úlohy,
číselného oboru a znázornění při výchozích čtrnácti úlohách.

Drží to dvě věci:

- **Velikosti jsou v CSS proměnných** (`--fruit-size`, `--eq-size`, `--box-size`)
  na prvku `#sheet`. Číselný obor se propisuje do atributu `data-range`, takže
  list do 20 kreslí ovoce menší než list do 5 — jinak by se dvojnásobek kusů
  na stránku nevešel.
- **Hustší typy dostanou menší ovoce a delší řadu.** „O kolik víc" a „doplň
  chybějící číslo" mají v obrázku dvě řady hromádek, proto skládají ovoce po
  deseti místo po pěti (`--pile-cols`). U „o kolik víc" to navíc pomáhá — dvě
  řady po deseti jdou porovnat na pohled jako číselná osa.

Ověřené je to na nejhorších možných listech — takových, kde má každá úloha
maximální možné počty kusů pro daný obor. Nejvyšší z nich měří 986 px proti
1009 px, které na A4 zbývají po okrajích. Když si počet úloh zvýšíte nad
čtrnáct, list přeteče na druhou stránku; kartičky se ale nikdy nerozdělí přes
zlom.

# Struktura projektu

```
index.html            celá aplikace — HTML, CSS a JavaScript v jednom souboru
fonts/
  Bravura.otf         notopisný font Bravura
  Bravura.woff2       tentýž font ve webové variantě
  bravura_metadata.json  SMuFL metadata (rozměry znaků ve mezerách osnovy)
  OFL.txt             licence fontu
```

Aplikace nemá žádné externí závislosti a funguje offline.

# Licence

Font Bravura © 2020 Steinberg Media Technologies GmbH, šířený pod licencí
SIL Open Font License 1.1 — plný text v [fonts/OFL.txt](fonts/OFL.txt).
"Bravura" je Reserved Font Name podle této licence.

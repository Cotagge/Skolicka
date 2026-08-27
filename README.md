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
   list je formátovaný na A4.

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
| Odčítání | Hromádka s přeškrtnutými kusy (nebo dvě hromádky s mínus — viz níže) a příklad `a − b = ☐` |
| Sčítání i odčítání | Náhodný mix obou předchozích |
| Doplň znaménko | Jen čísla — `a ☐ b = výsledek`, dítě doplní `+` nebo `−` |
| Vše dohromady | Náhodný mix všech typů |

Volitelný je **číselný obor** (do 5, do 10, do 20), **znázornění**, **druh ovoce**
(jablka, hrušky, třešně, jahody, pomeranče, nebo náhodně u každé úlohy) a **počet
úloh** na listu.

## Znázornění

| Volba | Co je na kartičce |
|---|---|
| Ovoce i čísla | Hromádky ovoce a pod nimi číselný příklad |
| Jen ovoce | Pouze hromádky ovoce a prázdný zápis `☐ + ☐ = ☐` — dítě doplní i oba sčítance (menšence), čísla nikde nevidí předepsaná |
| Jen čísla | Pouze číselný příklad, bez obrázků (výběr ovoce se skryje) |

U typu **Doplň znaménko** se ovoce kreslí jen ve volbě „Jen ovoce" — hromádky `a`
a `b` s rámečkem mezi nimi a výsledná hromádka pod tím. Ve volbě „Ovoce i čísla"
by vznikly dva prázdné rámečky vedle sebe a nebylo by poznat, do kterého se píše
znaménko, proto tam zůstává jen číselný zápis.

## Odčítání s ovocem

Odčítání jde znázornit dvěma způsoby; přepínač **Odčítání** se objeví jen tehdy,
když list nějaké odčítání obsahuje a zároveň se kreslí ovoce.

| Volba | Jak úloha vypadá |
|---|---|
| Škrtání + doplň čísla | Jedna hromádka, posledních `b` kusů je přeškrtnutých. Obrázek odpovídá skutečné situaci — bylo `a` kusů, `b` se odebralo. |
| Dvě hromádky s mínus | Hromádka `a`, znaménko `−`, hromádka `b` — stejné schéma jako u sčítání. Dítě opravdu odčítá, ale na papíře je dohromady víc kusů, než kolik je menšenec. |

Ve volbě „Jen ovoce" má každá úloha trojici rámečků `☐ − ☐ = ☐`, respektive
`☐ + ☐ = ☐`. Kdyby bylo zadání jen `= ☐`, stačilo by u odčítání spočítat
nepřeškrtnuté kusy a k žádnému počítání příkladu by nedošlo. Takhle dítě doplní
i obě počítaná čísla — kolik kusů bylo, kolik se přidalo nebo odebralo a kolik
jich je nakonec.

Úlohy se generují tak, aby výsledek nikdy nebyl záporný ani nula a aby součet
nepřesáhl zvolený obor. Obě hromádky mají vždy aspoň jeden kus.

Ovoce je kreslené vektorově přímo v `index.html` (inline SVG), takže se tiskne
ostře v jakékoli velikosti a nepotřebuje žádné obrázkové soubory.

Nad úlohami je hlavička s názvem cvičení a řádkem na jméno a datum.

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

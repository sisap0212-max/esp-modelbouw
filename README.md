# esp-modelbouw

Software voor het **mini-billboard** voor modelbouw: een klein scherm dat foto's, korte video's
en teksten afwisselt, zoals een echt reclamebord. Je beheert het met je telefoon via de eigen
wifi van het billboard; je hebt geen app of internet nodig.

Bordje: ESP32-2432S022 (2,2 inch scherm, 320 × 240).

## Bestanden in deze map

| Bestand | Waarvoor |
|---|---|
| `billboard.bin` | De gewone software met alle functies. Billboards met thuis-wifi halen deze vanzelf op als het versienummer hoger is dan wat ze hebben. |
| `herstel.bin` | Een aparte herstelversie. Alleen te kiezen in de herstelmodus; wordt altijd geinstalleerd, ook als hij ouder is. |
| `billboard_eerste_installatie.bin` | Alles in één bestand (opstartcode + geheugenindeling + software) voor de eerste keer via USB. Niet voor online bijwerken. |
| **Releases** (rechts op GitHub) | Alle versies, ook oudere. Op de pagina van het billboard kies je er een uit met "Andere versie kiezen". Elke release heeft een bijlage `billboard.bin`. |

> De billboards lezen `billboard.bin` en `herstel.bin` rechtstreeks uit deze map (branch `main`).
> Hernoem of verplaats deze bestanden en deze repository dus niet: anders krijgen verkochte
> billboards geen updates meer.

## Het billboard gebruiken

1. **Stekker erin.** Het scherm laat twee QR-codes zien.
2. **Eerste keer:** verbind met de open wifi `Billboard-instellen` en kies een wachtwoord (en eventueel een naam).
3. **Daarna:** verbind met de wifi `Billboard` (of de naam die je koos). De pagina opent vanzelf; zo niet, ga naar `http://192.168.4.1`.
4. Zet er foto's, video's (max. 20 seconden), teksten of een stationsklok op. Op de pagina stel je ook de tijd per foto, de volgorde, de helderheid en de effecten in.

De wifi van het billboard blijft altijd aan.

### Thuis-wifi (hoeft niet)

Vul op de pagina onder **Thuis-wifi** de naam en het wachtwoord van je eigen wifi in. Dan:

- kun je het billboard thuis openen via `http://billboard.local` (inloggen met het wachtwoord van het billboard);
- zoekt het billboard bij elke keer aanzetten zelf naar een nieuwere versie;
- zie je op het scherm en bovenaan de pagina of hij verbonden is (✔ of ✖).

Lukt verbinden niet (bijvoorbeeld op een beurs), dan werkt alles gewoon zonder. Het billboard
probeert het elke 2 minuten opnieuw, maar alleen als er geen telefoon met het billboard verbonden is.

### Herstelmodus

Doe **3 keer snel** (binnen 10 seconden) de stekker erin en eruit, en laat hem de 3e keer zitten.
Het billboard gaat ook vanzelf in de herstelmodus als het 3 keer achter elkaar vastloopt.

Verbind dan met de open wifi `Billboard-herstel` en ga naar `http://192.168.4.1`. Daar kun je:

- via je thuis-wifi `billboard.bin`, `herstel.bin` of een andere versie uit de Releases (ook oudere) erop zetten;
- een `.bin`-bestand uploaden (ook een oudere versie);
- de vorige versie terugzetten;
- alle foto's wissen, of alles wissen;
- normaal opstarten.

Een andere versie kiezen (ook een oudere) kan op de gewone pagina én in de herstelmodus, onder
"Andere versie kiezen". Daarvoor moet het billboard met je thuis-wifi verbonden zijn.

### Alles wissen (terug naar fabrieksinstellingen)

Doe **5 keer snel** de stekker erin en eruit. Bij de 5e keer vraagt het scherm 10 seconden lang
"Alles wissen?". Haal de stekker eruit terwijl die vraag er staat en doe hem er weer in: alles wordt gewist.
Laat je hem zitten, dan gebeurt er niets.

## Voor de maker: een nieuwe versie uitbrengen

1. Verhoog `BB_VERSIE` bovenaan `billbo123ard.ino`.
   - Het billboard vergelijkt per stuk tussen de punten: `2.10` is nieuwer dan `2.9`, en `1.14` is nieuwer dan `1.6`.
   - De versies tot en met 1.14 zijn het oude formaat; de nieuwe reeks begint bij **2.0**.
   - Laat een getal na de punt nooit met een 0 beginnen (dus niet `2.05`).
   - Pas ook `NIEUW` aan (vlak onder `BB_VERSIE`): één korte regel per nieuwe functie, hooguit 6.
     Na de update staat dat lijstje 6 seconden op het scherm, en op de pagina onder "Wat is er nieuw".
2. Arduino IDE: board **ESP32 Dev Module**, **Extra → Partition Scheme → Custom**
   (dan gebruikt hij `partitions.csv` uit de schetsmap). Laat `partitions.csv` altijd naast de `.ino` staan.
3. Controleer na het compileren: "Sketch uses …" moet onder **1.572.864 bytes** blijven (1,5 MB).
4. **Schets → Gecompileerd binair bestand exporteren.** In de schetsmap, onder `build/esp32.esp32.esp32/`, komen dan:
   - `billbo123ard.ino.bin` → upload als **`billboard.bin`**
   - `billbo123ard.ino.merged.bin` → upload als **`billboard_eerste_installatie.bin`**
5. Upload de bestanden hier (zelfde namen, branch `main`). Billboards met thuis-wifi installeren
   de nieuwe versie de volgende keer dat ze aangaan, of meteen met de knop "Nieuwste versie zoeken".
6. Maak er ook een **Release** van, zodat hij in de keuzelijst komt:
   **Releases → Draft a new release** → tag `v2.1` (het versienummer met een v ervoor) →
   titel: kort wat er nieuw is → sleep `billboard.bin` (en eventueel `billboard_eerste_installatie.bin`)
   bij "Attach binaries" → **Publish release**. De bijlage moet precies `billboard.bin` heten.

Een nieuwe versie moet eerst 20 seconden goed draaien. Loopt hij eerder vast of herstart hij,
dan zet het billboard vanzelf de vorige versie terug.

### Herstelversie

`herstel.bin` maak je op dezelfde manier (stap 4, het bestand zonder "merged"). Het moet wel
software van dit billboard zijn (met `BBVERSIE`), anders weigert het billboard het.

### Eerste installatie via USB

Zet `billboard_eerste_installatie.bin` op adres **0x0**, bijvoorbeeld met
[esptool-js](https://espressif.github.io/esptool-js/) in Chrome of Edge (Connect → adres `0x0`
→ bestand kiezen → Program), of met esptool:

```
esptool.py --chip esp32 write_flash 0x0 billboard_eerste_installatie.bin
```

Let op: bij een bordje dat al software had met een andere geheugenindeling worden de foto's
daarbij één keer gewist. Daarna blijven ze bij elke update staan.

## Geheugenindeling (`partitions.csv`)

| Deel | Grootte | Waarvoor |
|---|---|---|
| nvs | 20 KB | instellingen en wachtwoorden |
| otadata | 8 KB | welke software-plek actief is |
| app0 / app1 | 2 × 1,5 MB | twee software-plekken (nieuwe versie + reserve) |
| spiffs | 960 KB | foto's, video's en teksten |

Deze indeling kan na verkoop niet meer via een update veranderen.

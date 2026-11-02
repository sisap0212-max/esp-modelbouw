# Wat is er per versie bijgekomen

Een overzicht van elke functie die is toegevoegd of veranderd. De nieuwste versie staat bovenaan.

## 2.6 — wifi, mooiere klok (nieuwste)

- **Terug naar wifi, Bluetooth er volledig uit.** Het bordje maakt weer zijn eigen wifi met de
  bedienpagina op het bordje zelf (`http://192.168.4.1`). Werkt op elke telefoon zonder app.
- **Mooiere stationsklok:** gladde (anti-aliased) randen in plaats van blokjes, net als een echte
  stationsklok. Overgenomen uit 2.5.
- **C3-scherm goed rechtop** (gedraaid en 2 pixel verschoven, zodat er geen streepje aan de rand staat).
- **Alles wissen kan nooit meer per ongeluk via de stekker.** Alleen nog bewust: ingelogd op de
  pagina, of in de herstelmodus.

## 2.5 — mooiere klok (Bluetooth)

- **Mooiere stationsklok** (gladde randen).
- **Herstelmodus met grote knoppen:** Repareren en Normaal opstarten.
- **Werkt ook zonder internet:** de pagina werkt ook offline nadat hij één keer is geopend.
- **Duidelijke melding** als er geen internet is.

## 2.4 — Bluetooth (deze versie is vervangen door 2.6)

- **Bediening via Bluetooth** in plaats van wifi, via een bedienpagina op internet (GitHub Pages).
- **Vooruitkijken met het weer:** de pagina stuurde de verwachting per uur voor 3 dagen mee, het
  bordje koos zelf het juiste uur.
- Kleinste software (geen wifi), maar wel een app nodig op de iPhone (Bluefy).

## 2.3 — wifi (basis van 2.6)

- **Afspeellijsten:** Zomer, Kerst, Beurs... en met één tik wisselen.
- **Nieuwe, mooiere bedienpagina** (ook een donkere stand).
- **Foto's 17% en video's 25% kleiner**, dus er passen er meer op.
- **Zoeken naar updates kijkt ook naar de GitHub-releases.**
- **Werkt ook op de C3 SuperMini** met het 1,8"-scherm.

## Oudere versies (tot en met 1.14)

De eerste versies met foto's, video, tekst-dia's, de stationsklok, het weer, samen wisselen en de
eerste wifi-bediening.

---

# Alle functies op een rij (versie 2.6)

| Functie | Wat het doet |
|---|---|
| Foto's en video's | Diashow van foto's en korte video's. |
| Tekst-dia's | Eigen tekst met zelf gekozen kleuren. |
| Stationsklok | Klassieke klok met gladde wijzers; tijd van internet of van de telefoon. |
| Weer-dia | Het weer van vandaag (via de thuis-wifi). |
| Afspeellijsten | Groepen dia's (Zomer, Kerst, Beurs...), met één tik wisselen. |
| Samen wisselen | Meerdere bordjes tegelijk, Leider/Volger via ESP-NOW (zonder router). |
| Eigen wifi + pagina | Bediening via `192.168.4.1`, geen app nodig, tot 4 telefoons tegelijk. |
| Thuis-wifi (optioneel) | Internet voor klok, weer en updates. |
| Wachtwoord en naam | Eigen wachtwoord (WPA2) en een eigen naam voor het bordje. |
| Software bijwerken | Nieuwe versie ophalen van GitHub, alleen als het nummer hoger is. |
| Terugval op vorige versie | Werkt een update niet binnen 20 s, dan komt de vorige versie terug. |
| Herstelmodus | 3x de stekker, of 3x vastlopen: open herstel-wifi om te repareren. |
| Alles wissen | Alleen bewust (ingelogd of in de herstelmodus), nooit per ongeluk. |
| Effecten | Neon-flikker en een zwarte pauze tussen dia's. |
| Twee bordjes | Dezelfde code voor het 2,2-inch bordje en de C3 SuperMini (1,8"). |

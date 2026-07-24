# Písmena

PWA aplikace pro výuku písmen abecedy. Po stisku klávesy se dané písmeno zobrazí přes celou obrazovku a zároveň se přečte nahlas.

## Použití

Stiskni libovolnou klávesu A–Z. Aplikace:
1. Zobrazí písmeno velkým písmem přes celou obrazovku
2. Přečte jeho název nahlas (např. K → „ká", L → „el")
3. Po 3 sekundách písmeno zmizí

Určeno pro použití s fyzickou klávesnicí — na počítači nebo na mobilu/tabletu s připojenou bezdrátovou klávesnicí.

## Technologie

### Web Speech API — syntéza řeči
Řeč probíhá přímo v prohlížeči pomocí `window.speechSynthesis`, nevyžaduje žádný backend ani síťové připojení. Každé písmeno má přiřazen svůj český název při hláskování (např. B → „bé", R → „er") — tím se předejde nežádoucí výslovnosti, kterou by syntetizér zvolil pro samotné písmeno. Jazyk utterance je nastaven na `cs-CZ`, tempo řeči je mírně zpomaleno (`rate: 0.8`). Před každým novým přečtením se případná předchozí promluva zruší (`cancel()`), aby nedocházelo k hromadění fronty při rychlém stisku více kláves.

### Zobrazení
Velikost písmene je nastavena pomocí `min(80vw, 80vh)` — vždy zabere 80 % kratší strany obrazovky, ať je orientace jakákoliv. Písmeno se objeví s krátkou animací (opacity + scale). Pokud je stejná klávesa stisknuta opakovaně, animace se resetuje. Hint „Stiskni klávesu A–Z" se při prvním stisku trvale skryje.

### PWA — Progressive Web App
Aplikace obsahuje `manifest.json` a service worker (`sw.js`), díky čemuž ji lze nainstalovat na plochu telefonu nebo počítače přes prohlížeč. Service worker cachuje všechny soubory při první návštěvě, takže aplikace funguje i offline.

## Soubory

| Soubor | Popis |
|---|---|
| `index.html` | Celá aplikace — HTML struktura, CSS styly i JavaScript logika v jednom souboru |
| `manifest.json` | Manifest pro PWA: název, barvy, ikony, režim zobrazení (`fullscreen`) |
| `sw.js` | Service worker — při instalaci cachuje soubory aplikace, při fetch požadavcích vrací cache, při aktivaci maže staré verze cache |

# C21-borden & bereikbaarheid — Amsterdam

Twee kaarten die vrachtverkeer met een RVV-ontheffing helpen zien **welke gewichtsborden voor hén gelden** en **waar hun voertuig kan komen**.

**Live:**
- Bordenkaart → https://jess-gearbox.github.io/c21-amsterdam/index.html
- Bereikbaarheidskaart → https://jess-gearbox.github.io/c21-amsterdam/bereikbaarheid.html

## De twee kaarten

**Bordenkaart** (`index.html`) — alle C21-gewichtsborden in Amsterdam, met onderscheid tussen de **7,5t-zone** (waar een ontheffing geldt) en de **losse C21-borden** die wél voor je gelden. Filter op gewicht, zonetype en status.

**Bereikbaarheidskaart** (`bereikbaarheid.html`) — welke wegvakken wel/niet bereikbaar zijn voor een specifiek vrachtwagenprofiel, met de 7,5t-zone er zichtbaar overheen. Dagelijks automatisch bijgewerkt.

## Waarom

Met een RVV-ontheffing ben je vrijgesteld van de 7,5t-**zone**borden, maar niet van de overige C21-borden in de stad. Bestaande kaarten maken dat onderscheid niet zichtbaar — deze wel. En de bereikbaarheidskaart laat zien waar een zwaar voertuig überhaupt kan komen, zodat je die twee dingen kunt combineren.

## Databronnen

- **Verkeersborden:** NDW open data (`rvvCode=C21`, gemeente `GM0363`)
- **Bereikbaarheid:** NDW bereikbaarheids-API (accessibility-map)
- **Wegennet & luchtfoto:** PDOK — NWB Wegen en Luchtfoto
- **Basiskaart:** OpenStreetMap / CARTO

## Hoe het bijgewerkt wordt

De bordenkaart haalt de borden live bij NDW op. De bereikbaarheidskaart draait op een dagelijkse GitHub Action (`.github/workflows/update-accessibility.yml`): die berekent de bereikbaarheid server-side voor het profiel in `vehicle-request.json` en werkt het resultaat (`accessibility.geojson`) bij. Wijzig je een bord in NDW, dan loopt de kaart binnen een dag mee.

## Voertuigprofiel

Het profiel van de bereikbaarheidskaart staat in **`vehicle-request.json`** (nu: vrachtwagen, 22,5 t, aslast 10,5 t, 4 m hoog, 2,35 m breed, 8,25 m lang, diesel Euro 6). Aanpassen = dat bestand wijzigen; de volgende Action-run rekent het opnieuw.

## Status & volgende stappen

Dit is een MVP. Op de rol:
- Klik-op-de-kaart **puntcheck** — "kan ik hier komen, en zo nee waarom, en is het alleen de 7,5t-zone?"
- Zelf instelbaar voertuigprofiel (bijv. Leeg / Vol)

Beide vragen een klein tussenlaagje (proxy) voor de live-API.

## Let op

Borden **met een onderbord** (venstertijden, uitzonderingen) worden door de bereikbaarheids-API genegeerd en tellen als bereikbaar; afslagverboden tellen niet mee. De kaarten zijn een hulpmiddel, geen juridisch oordeel — controleer altijd je eigen ontheffingsvoorwaarden.

## Colofon

Een persoonlijk project, gebouwd om collega's te helpen. Kaart- en borddata © NDW, PDOK / Rijkswaterstaat, OpenStreetMap-bijdragers en CARTO.
